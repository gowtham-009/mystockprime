<template>
    <div class="card">
        <Toast  position="bottom-right" />
  
        <div style="display: flex; justify-content: center; margin-bottom: 2%;">
            <SelectButton v-model="size" :options="sizeOptions" optionLabel="label" dataKey="label" />
        </div>
        <ContextMenu ref="cm" :model="menuModel" @hide="selectedProduct = null" />
        <DataTable 
        ref="dt"
        stripedRows 
        scrollable
        scrollHeight="430px"
        v-model:selection="selectedProduct" 
        :size="size.value" 
        v-model:expandedRows="expandedRows" 
        v-model:filters="filters" 
        :value="filteredCustomers"  
        paginator
        :rows="rows" 
        dataKey="id"
        filterDisplay="menu"
        resizableColumns
         columnResizeMode="fit"
         showGridlines 
        @rowSelect="onRowSelect"
        @rowUnselect="onRowUnselect"     
        @rowExpand="onRowExpand" 
        @rowCollapse="onRowCollapse"  
        :globalFilterFields="['name', 'countries.name', 'representative.name', 'status']"
         contextMenu 
         v-model:contextMenuSelection="selectedProduct"
        @rowContextmenu="onRowContextMenu"
          class="custom-datatable"
        >
  
        <template #paginatorstart>
                <div style="display: flex; gap: 10px;">
                    <Button v-for="size in [10, 15, 20]" :key="size" :label="size" @click="rows = size" :class="{'p-button-primary': rows === size, 'p-button-outlined': rows !== size}" />
                </div>
            </template>
  
            <template #header>
               <div class="w-full flex justify-center gap-3">
                
                <IconField class="flex justify-start items-center" >
                        <InputIcon>
                            <i class="pi pi-search " />
                        </InputIcon>
                        <InputText v-model="filters['global'].value" placeholder="Search..." />
                    </IconField>
  
                    <MultiSelect
                v-model="selectedColumns"
                :options="columns"
                optionLabel="header"
                @change="updateVisibleColumns"
                display="template"
                label="Show/Hide Columns"
                :showToggleAll="false"
              >
                <template #value>
                  Show/Hide Columns
                </template>
                <template #footer v-if="showReset">
                  <Button label="Reset" style="width: 100%;" @click="resetColumns"/>
                </template>
              </MultiSelect>
  
              <MultiSelect 
              v-model="selectedStatuses" 
               :showToggleAll="false"
                :options="statusesFilter"
                 placeholder="Filter by Status"
                  @change="filterByStatus" 
                  display="chip" >
                  <template #footer v-if="filterReset">
                  <Button label="Reset" @click="resetFilter" style="width: 100%;"/>
                </template>
                </MultiSelect>
  
                <Button icon="pi pi-external-link" label="Export" @click="exportSelectedCSV" />
  
                <Button label="New" icon="pi pi-plus" severity="contrast" @click="visiblerecord()"  />
                <Button label="Delete" icon="pi pi-trash" severity="danger"  outlined @click="deleterows" />
              <Button icon="pi pi-refresh" severity="contrast"  @click="reload()" rounded raised />
  
            
  
                
             
  
          
               
               </div>
            </template>
            <template #empty> No customers found. </template>
            <Column  selectionMode="multiple" headerStyle="width: 3rem"></Column>
            <Column  header="Expand" expander  />
            <Column  v-if="visibleColumns.includes('name')"  field="name" header="Name" exportHeader="Name" sortable :exportable="true" style="min-width: 14rem; cursor: pointer;">
                <template #body="{ data }"> <span @click="routePage(data)">{{ data.name }}</span></template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('countries.name')" field="countries.name" header="Country"  sortable sortField="countries.name" :exportable="true" filterField="countries.name" style="min-width: 14rem">
                <template #body="{ data }">
                    <div class="flex items-center gap-2">
                        <span>{{ data.countries.name }}</span>
                    </div>
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by country" />
                </template>
            </Column>
  
            <Column v-if="visibleColumns.includes('representative.name')" field="representative.name" header="Representative"  sortable sortField="representative.name" :exportable="true" filterField="representative" style="min-width: 14rem">
                <template #body="{ data }">
                    <div class="flex items-center gap-2">
                        <span>{{ data.representative.name }}</span>
                    </div>
                </template>
                <template #filter="{ filterModel }">
                    <MultiSelect v-model="filterModel.value" :options="representatives" optionLabel="name" placeholder="Any" />
                </template>
            </Column>
  
            <Column v-if="visibleColumns.includes('status')" field="status" header="Status" :exportable="true" sortable style="min-width: 12rem">
                <template #body="{ data }">
                    <Tag :value="data.status"  :severity="getSeverity(data.status)" />
                </template>
                <template #filter="{ filterModel }">
                    <Select v-model="filterModel.value" :options="statuses" placeholder="Select One" showClear />
                </template>
            </Column>
  
            <Column header="Action" style="min-width: 12rem;" :exportable="false">
                <template #body="slotProps">
                    <div style="display: flex; gap:5px">
                        <Button  icon="pi pi-eye" @click="modal(slotProps.data)" severity="info" raised rounded />
                        <Button  icon="pi pi-trash"  severity="danger" raised rounded />
                    </div>
                </template>
            </Column>
  
            <template #expansion="{ data }">
                <div v-if="data && Object.keys(data).length > 0" class="p-3">
                    <h3>Customer Details</h3>
                    <p><strong>Name:</strong> {{ data.name }}</p>
                    <p><strong>Country:</strong> {{ data.countries?.name || 'N/A' }}</p>
                    <p><strong>Representative:</strong> {{ data.representative?.name || 'N/A' }}</p>
                    <p><strong>Status:</strong> {{ data.status }}</p>
                </div>
                <div v-else class="p-3 text-center text-gray-500">
                    Data not available
                </div>
            </template>
        </DataTable>
  
        <Dialog v-model:visible="visible" maximizable modal header="Details" 
        :style="{ width: '30rem' }" :breakpoints="{ '1199px': '75vw', '575px': '90vw' }">
            <p class="m-0">
                <span>Name: {{ name }}</span> <br><br>
                <span>Country: {{ country }}</span> <br><br>
                <span>Representative: {{ rep }}</span> <br><br>
                <span>Status: {{ status }}</span> <br><br>
            </p>
        </Dialog>
  
        <Dialog v-model:visible="visiblerec" modal header="Edit Profile" :style="{ width: '25rem' }">
            <template #header>
                <div class="inline-flex items-center justify-center gap-2"> 
                    <h3 class="font-bold whitespace-nowrap">Add New Record</h3>
                </div>
            </template>
           
            <div style=" margin-bottom: 1%; display: flex; flex-direction: column;">
                <label for="username" class="font-semibold w-24">Name</label>
                <InputText id="username" class="flex-auto" autocomplete="off" />
            </div>
            <div style=" margin-bottom: 1%; display: flex; flex-direction: column;">
                <label for="username" class="font-semibold w-24">Country</label>
                <InputText id="username" class="flex-auto" autocomplete="off" />
            </div>
            <div style=" margin-bottom: 1%; display: flex; flex-direction: column;">
                <label for="username" class="font-semibold w-24">Representative</label>
                <InputText id="username" class="flex-auto" autocomplete="off" />
            </div>
            <div style=" margin-bottom: 1%; display: flex; flex-direction: column;">
                <label for="username" class="font-semibold w-24">Status</label>
                <InputText id="username" class="flex-auto" autocomplete="off" />
            </div>
            <template #footer>
                <Button label="Cancel" text severity="secondary" @click="recordeclose() " autofocus />
                <Button label="Save" outlined severity="secondary" @click="recordesave() " autofocus />
            </template>
        </Dialog>
  
  
  
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import { FilterMatchMode, FilterOperator } from '@primevue/core/api';
  import { useToast } from "primevue/usetoast";
  import { useRouter } from 'vue-router'
  
  import 'primeicons/primeicons.css'
  
  const toast = useToast();
  
  const selectedProduct = ref();
  
  const visible = ref(false);
  const rows = ref(10);
  const expandedRows = ref(null); 
  
  
  
  
  const columns = ref([
  
    { field: 'name', header: 'Name' },
    { field: 'countries.name', header: 'Country' },
    { field: 'representative.name', header: 'Representative' },
    { field: 'status', header: 'Status' }
  ]);
  
  
  
  const selectedColumns = ref([...columns.value]); // Default: all columns selected
    const visibleColumns = ref(columns.value.map(col => col.field)); // Tracks visibility
    const showReset = ref(false); // Controls visibility of Reset button
    
    const updateVisibleColumns = () => {
      visibleColumns.value = selectedColumns.value.map(col => col.field);
      showReset.value = selectedColumns.value.length < columns.value.length; // Show Reset only when some columns are unchecked
    };
    
    const resetColumns = () => {
      selectedColumns.value = [...columns.value]; // Reset selection
      updateVisibleColumns(); // Ensure UI updates
    };
    
    watch(selectedColumns, updateVisibleColumns, { deep: true });
  
  
  
    
  const size = ref({ label: 'Normal', value: 'null' });
  const sizeOptions = ref([
    { label: 'Small', value: 'small' },
    { label: 'Normal', value: 'null' },
    { label: 'Large', value: 'large' }
  ]);
  const representatives = ref([
    { name: 'Emily Tanka' },
    { name: 'Carlos Rivera' },
    { name: 'Olivia Smith' },
    { name: 'Noah Wilson' },
    { name: 'Ava Taylor'},
    { name: 'James Anderson' },
    { name: 'Charlotte Martinez' },
    { name: 'Benjamin Lopez' },
    { name: 'Evelyn Lee' },
    { name: 'William Brown' }
  ]);
  
  
  
  const customers = ref([]);
  const filters = ref({});
  
  const statuses = ref(['unqualified', 'qualified', 'new', 'negotiation', 'renewal', 'proposal']);
  
  const selectedStatuses = ref([]);
  const filterReset=ref(false)
    const statusesFilter = ref(['Unqualified', 'Qualified', 'New', 'Negotiation', 'Renewal', 'Proposal']);
    
    const filteredCustomers = computed(() => {
      if (selectedStatuses.value.length === 0) return customers.value;
      return customers.value.filter(customer => selectedStatuses.value.includes(customer.status));
    });
  
    watch(selectedStatuses, () => {
    filterReset.value = selectedStatuses.value.length > 0;
  });
  
  const resetFilter = () => {
    selectedStatuses.value = [];
    filterReset.value = false;
  };
  
  
  
  
  const filterByStatus = () => {
    toast.add({ severity: 'info', summary: 'Status Filter Applied', detail: selectedStatuses.value.join(', '), life: 3000 });
  };
  
  const postData = async () => {
    try {
        const res = await fetch('/table.json');
        if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
        customers.value = await res.json();
    } catch (error) {
        console.error("Error:", error.message);
    }
  };
  
  onMounted(() => {
    postData();
  });
  
  const initFilters = () => {
    filters.value = {
        global: { value: null, matchMode: FilterMatchMode.CONTAINS },
        name: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        'countries.name': { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        representative: { value: null, matchMode: FilterMatchMode.IN },
        status: { operator: FilterOperator.OR, constraints: [{ value: null, matchMode: FilterMatchMode.EQUALS }] }
    };
  };
  
  initFilters();
  
  
  
  const getSeverity = (status) => {
    switch (status) {
        case 'unqualified': return 'error';
        case 'qualified': return 'success';
        case 'new': return 'info';
        case 'negotiation': return 'warn';
        case 'renewal': return null;
        default: return null;
    }
  };
  
  const name = ref('');
  const country = ref('');
  const rep = ref('');
  const status = ref('');
  
  const modal = (values) => {
    
    visible.value = true;
    name.value = values.name;
    country.value = values.countries?.name || 'N/A';
    rep.value = values.representative?.name || 'N/A';
    status.value = values.status;
    toast.add({ severity: 'success', summary: `Viewed ${values.name}` , life: 3000 });
  };
  
  const onRowExpand = (event) => {
    if (expandedRows.value && expandedRows.value === event.data.id) {
        expandedRows.value = null;
    } else {
        expandedRows.value = event.data.id;
    }
  };
  
  const onRowCollapse = (event) => {
    expandedRows.value = null;
  };
  
  const dt = ref();
  
  const exportSelectedCSV = () => {
   
    if (selectedProduct.value && selectedProduct.value.length > 0) {
       
        toast.add({ severity: 'success', summary: 'Successfully Exported' , life: 3000 });
        dt.value.exportCSV({ selectionOnly: true });
       
    } else {
        toast.add({ severity: 'success', summary: 'Successfully Exported', life: 3000 });
        dt.value.exportCSV(); 
    }
  };
  const visiblerec=ref(false)
  const visiblerecord=()=>{
  
    visiblerec.value=true
  }
  
  const recordeclose=()=>{
    visiblerec.value=false
  }
  
  const recordesave=()=>{
    toast.add({ severity: 'success', summary: 'Success Message', detail:'Successfully Added Record', life: 3000 });
    visiblerec.value=false
  }
  
  const deleterows=()=>{
  
    try {
        const rowlen=selectedProduct.value
        if(rowlen.length>0){
            const selectrows=  selectedProduct.value.map(item => ({ id: item.id, name: item.name }));
            const dummarr=[]
            for(var i=0; i<selectrows.length; i++){
                   dummarr.push(selectrows[i].name)
                 }
            let constr=dummarr.toString()
            toast.add({ severity: 'success', summary: 'Success Rows Deleted', detail: constr, life: 3000 });
      
        }
        else{
            toast.add({ severity: 'error', summary: 'Please Select Rows', life: 3000 });
        }
    } catch (error) {
        toast.add({ severity: 'error', summary: 'Please Select Rows', life: 3000 });
       
        
    }
  }
  const cm = ref();
  
  const onRowSelect = (event) => {
    toast.add({ severity: 'info', summary: 'Product Selected', detail: 'Name: ' + event.data.name, life: 3000 });
  };
  const onRowUnselect = (event) => {
    toast.add({ severity: 'warn', summary: 'Product Unselected', detail: 'Name: ' + event.data.name, life: 3000 });
  }
  
  const menuModel = ref([
    {label: 'View', icon: 'pi pi-fw pi-search', command: () => viewProduct(selectedProduct)}
   
  ]);
  const onRowContextMenu = (event) => {
    cm.value.show(event.originalEvent);
  };
  const viewProduct = (product) => {
    toast.add({severity: 'info', summary: 'Product Selected', detail: product.value.name, life: 3000});
  };
  
  const router = useRouter();
  
  const routePage = (dataval) => {
    
    router.push('/demo')
    
  }
  
  
  const reload=()=>{
  
    initFilters();
    selectedProduct.value=[]
    resetColumns()
    resetFilter()
  }
  </script>
  
  
  <style>
  
  </style>
  
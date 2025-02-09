<template>
    <div class="card">
        <DataTable
          stripedRows 
        v-model:filters="filters" 
        v-model:selection="selectedCustomers"
         :value="filteredCustomers" 
         dataKey="id" filterDisplay="menu"
         scrollable 
         scrollHeight="600px"
         paginator
         :rows="rows" 
         ref="dt"
       
         :globalFilterFields="['stockname', 'quantity', 'avgprice', 'ltp', 'invamt', 'mktval', 'overall', 'days', 'date']"
          tableStyle="min-width: 50rem">
          <template #paginatorstart>
                <div style="display: flex; gap: 10px;">
                    <Button v-for="size in [10, 15, 20]" :key="size" :label="size" @click="rows = size" :class="{'p-button-primary': rows === size, 'p-button-outlined': rows !== size}" />
                </div>
            </template>

            <template #header>
               <div class="w-100 flex justify-start gap-2">
               
               
               <IconField>
                   <InputIcon>
                       <i class="pi pi-search" />
                   </InputIcon>
                   <InputText v-model="filters['global'].value" placeholder="Search stock and company" />
               </IconField>
               <DatePicker v-model="dates" selectionMode="range" :manualInput="false" dateFormat="yy-mm-dd" showIcon />
             
             
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
            
              <Button icon="pi pi-external-link" label="Export" @click="exportCSV($event)" />
            </div>

            </template>
            <template #empty> No customers found. </template>


           
            <Column v-if="visibleColumns.includes('stockname')" field="stockname" sortable header="Stockname"  exportHeader="Stockname">
                <template #body="{ data }">
            {{ data.stockname }}
        </template>
        <template  #filter="{ filterModel }">
            <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
        </template>
            </Column>
           
            <Column v-if="visibleColumns.includes('quantity')" field="quantity" sortable header="Quantity">
                <template #body="{ data }">
            {{ data.quantity }}
        </template>
        <template #filter="{ filterModel }">
            <InputText v-model="filterModel.value" type="text" placeholder="Search by quantity" />
            <Slider v-model="filterModel.value" class="w-full mt-3" />
        </template>
            </Column>
            <Column v-if="visibleColumns.includes('avgprice')" field="avgprice" sortable header="Avgprice">
                <template #body="{ data }">
            {{ data.avgprice }}
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('ltp')" field="ltp" sortable header="Ltp">
                <template #body="{ data }">
                    {{ data.ltp }}
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('invamt')" field="invamt" sortable header="Invamt">
                <template #body="{ data }">
                    {{ data.invamt }}
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('mktval')" field="mktval" sortable header="Mktval">
                <template #body="{ data }">
                    {{ data.mktval }}
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('overall')" field="overall" sortable header="Overall">
                <template #body="{ data }">
                    {{ data.overall }}
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('days')" field="days" sortable header="Days">
                <template #body="{ data }">
                    {{ data.days }}
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column field="date" sortable header="date" class="hidden"></Column>

          
        </DataTable>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import DatePicker from 'primevue/datepicker';
import { FilterMatchMode, FilterOperator } from '@primevue/core/api';
import Slider from 'primevue/slider';
import 'primeicons/primeicons.css'

const selectedCustomers = ref();
const filters = ref();

  const rows = ref(10);
const dates = ref([]);
const customers = ref([]);

const filteredCustomers = computed(() => {
    if (!dates.value || dates.value.length !== 2) {
        return customers.value;
    }
    
    const startDate = new Date(dates.value[0]);
    const endDate = new Date(dates.value[1]);
    endDate.setHours(23, 59, 59, 999); // Ensure end date includes all records of that day

    return customers.value.filter(customer => {
        const customerDate = new Date(customer.date);
        return customerDate >= startDate && customerDate <= endDate;
    });
});

const getdata = async () => {
    try {
        const res = await fetch('/sharetable.json');
        if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
        customers.value = await res.json();
    } catch (error) {
        console.error("Error:", error.message);
    }
};

onMounted(() => {
    getdata();
});


const initFilters = () => {
    filters.value = {
        global: { value: null, matchMode: FilterMatchMode.CONTAINS },
        stockname: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        quantity: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        avgprice: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        ltp: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        invamt: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        mktval: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        overall: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        days: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
       

    };
};

initFilters();

const columns = ref([
  
    { field: 'stockname', header: 'Stockname' },
    { field: 'quantity', header: 'Quantity' },
    { field: 'avgprice', header: 'Avgprice' },
    { field: 'ltp', header: 'Ltp' },
    { field: 'invamt', header: 'Invamt' },
    { field: 'mktval', header: 'Mktval' },
    { field: 'overall', header: 'Overall' },
    { field: 'days', header: 'Days' },

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
  

const dt=ref()
const exportCSV = () => {
 
    dt.value.exportCSV();
};
</script>

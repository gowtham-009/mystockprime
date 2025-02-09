<template>
         <Toast />
    <div class="overflow-hidden rounded-lg bg-white shadow">
      <div class="px-2 py-2 flex justify-center gap-3">
        <Button label="Week" :class="{ 'bg-blue-500 text-white': activeFilter === 'week' }" severity="secondary" variant="outlined" @click="filterLastWeek" />
        <Button label="15 Days" :class="{ 'bg-blue-500 text-white': activeFilter === '15days' }" severity="secondary" variant="outlined" @click="filterLast15Days" />
        <Button label="Month" :class="{ 'bg-blue-500 text-white': activeFilter === 'month' }" severity="secondary" variant="outlined" @click="filterLastMonth" />
        <Button label="3 Months" :class="{ 'bg-blue-500 text-white': activeFilter === '3months' }" severity="secondary" variant="outlined" @click="filterLast3Months" />
        <Button label="Customs" :class="{ 'bg-blue-500 text-white': activeFilter === 'customs' }" @click="customs"  severity="secondary" variant="outlined" />
      </div>
    </div>
  
    <div v-if="loading" class="w-full mt-5">
      <div class="overflow-hidden rounded-lg bg-white shadow" >
      <div class="px-12 py-2 flex animate-pulse">
        <div class="w-full p-1 flex" style="border-right: 2px solid rgb(189, 189, 189);">
          <div class="flex justify-center items-center p-1">
            <div class="h-12 w-12 bg-slate-300 rounded-full"></div>
          </div>
          <div class="w-full p-1">
            <div class="h-4 bg-slate-300 rounded w-2/3 mb-2"></div>
            <div class="h-6 bg-slate-300 rounded w-1/2"></div>
          </div>
        </div>
        <div class="w-full p-1 flex" style="border-right: 2px solid rgb(189, 189, 189);">
          <div class="flex justify-center items-center p-1">
            <div class="h-12 w-12 bg-slate-300 rounded-full"></div>
          </div>
          <div class="w-full p-1">
            <div class="h-4 bg-slate-300 rounded w-2/3 mb-2"></div>
            <div class="h-6 bg-slate-300 rounded w-1/2"></div>
          </div>
        </div>
        <div class="w-full p-1 flex" style="border-right: 2px solid rgb(189, 189, 189);">
          <div class="flex justify-center items-center p-1">
            <div class="h-12 w-12 bg-slate-300 rounded-full"></div>
          </div>
          <div class="w-full p-1">
            <div class="h-4 bg-slate-300 rounded w-2/3 mb-2"></div>
            <div class="h-6 bg-slate-300 rounded w-1/2"></div>
          </div>
        </div>
        <div class="w-full p-1 flex">
          <div class="flex justify-center items-center p-1">
            <div class="h-12 w-12 bg-slate-300 rounded-full"></div>
          </div>
          <div class="w-full p-1">
            <div class="h-4 bg-slate-300 rounded w-2/3 mb-2"></div>
            <div class="h-6 bg-slate-300 rounded w-1/2"></div>
          </div>
        </div>
      </div>
    </div>


    <div class="space-y-4 p-4 mt-5" >
              <!-- Table Skeleton -->
              <div class="grid grid-cols-9 gap-4 animate-pulse">
                <!-- Rows -->
                <!-- Row 1 -->
                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>
            
                <!-- Row 2 -->
                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>
            
                <!-- Row 3 -->
                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>
                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>
                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>
                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>
                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>

                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>

                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>
                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>

                <div class="col-span-9 grid grid-cols-9 gap-4">
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                  <div class="h-6 bg-gray-300 rounded col-span-1"></div>
                </div>
              </div>
            </div>
    </div>
 
    
    <div class="w-100" v-if="content">
        <div class="overflow-hidden rounded-lg bg-white shadow mt-1">
    <div class="px-2 py-3 ">
        <ul role="list" class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-4">

  <li class="col-span-1  rounded-lg bg-white shadow">
    <div class="flex w-full items-center justify-between space-x-6 p-2">
      <div class="flex truncate">
             <div class="flex justify-center items-center p-3 bg-indigo-50 rounded-full"  >
                  <img src="https://cdn-icons-png.flaticon.com/128/16416/16416833.png" alt="" width="40" height="40">
              </div>
              <div class="w-full p-1" >
                  <span class="text-slate-400 text-md">Invested Amount</span>
                 <p class="text-slate-700"> <span><i class="pi pi-indian-rupee"></i></span> <span >{{ investamount }}</span></p>
              </div>
      </div>
    </div>
    <div>
      
    </div>
  </li>

  <li class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow">
    <div class="flex w-full items-center justify-between space-x-6 p-2">
      <div class="flex truncate">
        <div class="flex justify-center items-center p-3 bg-indigo-50 rounded-full"  >
                  <img src="https://cdn-icons-png.flaticon.com/128/16416/16416833.png" alt="" width="40" height="40">
              </div>
              <div class="w-full p-1" >
                  <span class="text-slate-400 text-md">Current Value</span>
                 <p class="text-slate-700"><span><i class="pi pi-indian-rupee"></i></span> <span >{{ currentvalue }}</span></p>
              </div>
      </div>
    </div>
    <div>
      
    </div>
  </li>


  <li class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow">
    <div class="flex w-full items-center justify-between space-x-6 p-2">
      <div class="flex truncate">
        <div class="flex justify-center items-center p-3 bg-green-50 rounded-full"  >
                  <img src="https://cdn-icons-png.flaticon.com/128/5501/5501360.png" alt="" width="40" height="40">
              </div>                
              <div class="w-full p-1" >
                  <span class="text-slate-400 text-md">Overall Gain</span>
                  <p  class="text-slate-700"> <span><i class="pi pi-indian-rupee"></i></span> <span >{{ overallgain }}</span></p>
              </div>
      </div>
    </div>
    <div>
      
    </div>
  </li>

  <li class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow">
    <div class="flex w-full items-center justify-between space-x-6 p-2">
      <div class="flex truncate">
        <div class="flex justify-center items-center p-3 bg-green-50 rounded-full"  >
                  <img src="https://cdn-icons-png.flaticon.com/128/5501/5501360.png" alt="" width="40" height="40">
              </div>              
               <div class="w-full p-1" >
                  <span class="text-slate-400 text-md">Today's Gain</span>
                  <p  class="text-slate-700"> <span><i class="pi pi-indian-rupee"></i></span> <span >{{ todaygain }}</span></p>
               </div>
       
      </div>
    </div>
    <div>
      
    </div>
  </li>

</ul>
    </div>
  </div>



    <div class="overflow-hidden rounded-lg bg-white shadow mt-1">
      <div class="px-2 py-3 ">
        <div class="card">
          <DataTable
            stripedRows
            ref="dt"
            v-model:filters="filters"
            :value="filteredCustomers"
            dataKey="id"
            filterDisplay="menu"
            scrollable
            scrollHeight="400px"
            paginator
            :rows="rows" 
            tableStyle="min-width: 20rem"
            :globalFilterFields="['stockname', 'quantity', 'avgprice', 'ltp', 'invamt', 'mktval', 'overall', 'days', 'date']"

          >

          <template #header>
               <div class="w-100 flex justify-start items-center gap-2">
               <IconField>
                   <InputIcon>
                       <i class="pi pi-search" />
                   </InputIcon>
                   <InputText v-model="filters['global'].value" placeholder="Search stock and company" />
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

               <Button icon="pi pi-external-link" label="Export" @click="exportCSV($event)" />

             
            </div>

            </template>
            

          <template #paginatorstart>
                <div style="display: flex; gap: 10px;">
                    <Button v-for="size in [10, 50, 100]" :key="size" :label="size" @click="rows = size" :class="{'p-button-primary': rows === size, 'p-button-outlined': rows !== size}" />
                </div>
            </template>
          
         <template #empty> No customers found. </template>
            <Column  v-if="visibleColumns.includes('stockname')" field="stockname" sortable header="Stockname" exportHeader="Product Code">
                <template #body="{ data }">
                    {{ data.stockname }}
                </template>
                <template  #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by Stock name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('quantity')" field="quantity" sortable header="Quantity" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    {{ data.quantity }}
                </template>
                <template #filter="{ filterModel }">
                  <Slider v-model="filterValue" range class="w-56 mt-2" :min="8" :max="100" />
                  <div class="w-full flex justify-between p-2 ">
                    <span>{{ filterValue[0] }}</span>
                    <span>{{ filterValue[1] }}</span>
                  </div>
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('avgprice')" field="avgprice" sortable header="Avgprice" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    {{ data.avgprice }}
                </template>
                <template #filter="{ filterModel }">
                  <Slider v-model="filterprice" range class="w-56 mt-2" :min="1" :max="1000" />
                  <div class="w-full flex justify-between p-2 ">
                    <span>{{ filterprice[0] }}</span>
                    <span>{{ filterprice[1] }}</span>
                  </div>
                </template>
            </Column>
            <Column  v-if="visibleColumns.includes('ltp')" field="ltp" sortable header="LTP" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    {{ data.ltp }}
                </template>
                <template  #filter="{ filterModel }">
                  <Slider v-model="filterltp" range class="w-56 mt-2" :min="1" :max="1000" />
                  <div class="w-full flex justify-between p-2 ">
                    <span>{{ filterltp[0] }}</span>
                    <span>{{ filterltp[1] }}</span>
                  </div>
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('invamt')" field="invamt" sortable header="Invamt" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    {{ data.invamt }}
                </template>
                <template  #filter="{ filterModel }">
                  <Slider v-model="filterinv" range class="w-56 mt-2" :min="1" :max="1000" />
                  <div class="w-full flex justify-between p-2 ">
                    <span>{{ filterinv[0] }}</span>
                    <span>{{ filterinv[1] }}</span>
                  </div>
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('mktval')" field="mktval" sortable header="Mktval" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    {{ data.mktval }}
                </template>
                <template  #filter="{ filterModel }">
                  <Slider v-model="filtermkt" range class="w-56 mt-2" :min="1000" :max="50000" />
                  <div class="w-full flex justify-between p-2 ">
                    <span>{{ filtermkt[0] }}</span>
                    <span>{{ filtermkt[1] }}</span>
                  </div>
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('overall')" field="overall" sortable header="Overall" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    {{ data.overall }}
                </template>
                <template  #filter="{ filterModel }">
                  <Slider v-model="filteroverall" range class="w-56 mt-2" :min="1" :max="1000" />
                  <div class="w-full flex justify-between p-2 ">
                    <span>{{ filteroverall[0] }}</span>
                    <span>{{ filteroverall[1] }}</span>
                  </div>
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('days')" field="days" sortable header="Days" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    {{ data.days }}
                </template>
                <template  #filter="{ filterModel }">
                  <Slider v-model="filterdays" range class="w-56 mt-2" :min="1" :max="1000" />
                  <div class="w-full flex justify-between p-2 ">
                    <span>{{ filterdays[0] }}</span>
                    <span>{{ filterdays[1] }}</span>
                  </div>
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('date')" field="date" sortable header="Date" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    {{ data.date }}
                </template>
                <template  #filter="{ filterModel }">
                  <DatePicker 
      v-model="filters.date.constraints[0].value" 
      dateFormat="yy-mm-dd" 
      showIcon
      @update:modelValue="applyDateFilter"
    />
                </template>
            </Column>
            <Column   v-if="visibleColumns.includes('action')"  field="action" header="Action" :showFilterOperator="false" :showFilterMatchModes="false">
                <template #body="{ data }">
                    <Button icon="pi pi-eye" severity="info" @click="rightcanva(data)" class="p-0" variant="text" raised  />
                </template>
               
           </Column>

          </DataTable>

          <Dialog v-model:visible="visible" modal header="Date Range Filter" :style="{ width: '25rem' }" >
          
              <div class="w-100 flex justify-center gap-2">
                <DatePicker v-model="dates" selectionMode="range" :manualInput="true" dateFormat="yy-mm-dd" showIcon @update:modelValue="handleDateChange" />
              </div>
          
        </Dialog>

        <Drawer v-model:visible="visibleRight" header="Stock Details" position="right" class="!w-full md:!w-80 lg:!w-[80rem]">
          <div class="w-full p-1 flex flex-col h-full justify-between" >
            <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <thead>
              <tr>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">STOCK NAME</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">DATE</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">QUANTITY</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">AVERAGE PRICE</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">LTP</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">INVAMT</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">MKTVAL</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">OVERALL</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">DAYS</th>





              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
              <tr >
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{stockname}}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{dateval}}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{quant}}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{avg}}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ltp}}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{invamt}}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{mktval}}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{overall}}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{days}}</td>

              </tr>
            </tbody>
          </table>
        </div>
        <div class="w-full p-1 flex justify-center gap-2" >
            <Button label="Proceed" severity="success" @click="proceedfun" raised />
            <Button label="Cancel" severity="danger" @click="cancelfun" variant="outlined" />
        </div>
          </div>
        </Drawer>
        </div>
      </div>
    </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed, onMounted, watch  } from 'vue';
  import { FilterMatchMode, FilterOperator } from '@primevue/core/api';
  import Slider from 'primevue/slider';
  import DatePicker from 'primevue/datepicker';
  import 'primeicons/primeicons.css';
  import { useToast } from "primevue/usetoast";



  const loading=ref(true)
  const content=ref(false)

  const investamount=ref('')
  const currentvalue=ref('')
  const overallgain=ref('')
  const todaygain=ref('')

  const visibleRight = ref(false);
  const rows = ref(10);
  const dates = ref([]);
  const customers = ref([]);
  const activeFilter = ref('week');
  const visible = ref(false);
  const filters = ref({});
  const toast = useToast();

const minquant = ref(8);
const maxquant = ref(100);
const filterValue = ref([minquant.value, maxquant.value]);


const minprice=ref(1)
const maxprice=ref(1000)
const filterprice=ref([minprice.value, maxprice.value])

const minltp=ref(1)
const maxltp=ref(1000)
const filterltp=ref([minltp.value, minltp.value])

const mininv=ref(1)
const maxinv=ref(1000)
const filterinv=ref([mininv.value, maxinv.value])

const minmkt=ref(1000)
const maxmkt=ref(50000)
const filtermkt=ref([minmkt.value, maxmkt.value])

 const minoverall=ref(1)
 const maxoverall=ref(1000)
 const filteroverall=ref([minoverall.value, maxoverall.value])

 const mindays=ref(1)
 const maxdays=ref(1000)
 const filterdays=ref([mindays.value, maxdays.value])

 const datecol=ref()
const initFilters = () => {
  filters.value = {
    global: { value: null, matchMode: FilterMatchMode.CONTAINS },
    stockname: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
    quantity: { 
      operator: FilterOperator.AND, 
      constraints: [{ value: [minquant.value, maxquant.value], matchMode: FilterMatchMode.BETWEEN }] 
    },
    avgprice: { 
      operator: FilterOperator.AND, 
      constraints: [{ value: [minprice.value, maxprice.value], matchMode: FilterMatchMode.BETWEEN }] 
    },

    ltp: { 
      operator: FilterOperator.AND, 
      constraints: [{ value: [minltp.value, maxltp.value], matchMode: FilterMatchMode.BETWEEN }] 
    },

    invamt: { 
      operator: FilterOperator.AND, 
      constraints: [{ value: [mininv.value, maxinv.value], matchMode: FilterMatchMode.BETWEEN }] 
    },

    mktval: { 
      operator: FilterOperator.AND, 
      constraints: [{ value: [minmkt.value, maxmkt.value], matchMode: FilterMatchMode.BETWEEN }] 
    },

    overall: { 
      operator: FilterOperator.AND, 
      constraints: [{ value: [minoverall.value, maxoverall.value], matchMode: FilterMatchMode.BETWEEN }] 
    },
    
    days: { 
      operator: FilterOperator.AND, 
      constraints: [{ value: [mindays.value, maxdays.value], matchMode: FilterMatchMode.BETWEEN }] 
    },
    
    
  
  
    date: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.EQUALS }] },
  };
};

const applyDateFilter = () => {
  if (filters.value.date.constraints[0].value) {
    let selectedDate = filters.value.date.constraints[0].value;
    filters.value.date.constraints[0].value = formatDate(selectedDate);
  }
};

const formatDate = (date) => {
  if (!date) return null;
  const d = new Date(date);
  return `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, "0")}-${String(d.getDate()).padStart(2, "0")}`;
};

watch(filterValue, (newValue) => {
  filters.value.quantity.constraints[0].value = newValue;
});

watch(filterprice, (newValue) => {
  filters.value.avgprice.constraints[0].value = newValue;
});

watch(filterltp, (newValue) => {
  filters.value.avgprice.constraints[0].value = newValue;
});

watch(filterinv, (newValue) => {
  filters.value.invamt.constraints[0].value = newValue;
});

watch(filtermkt, (newValue) => {
  filters.value.mktval.constraints[0].value = newValue;
});

watch(filteroverall, (newValue) => {
  filters.value.overall.constraints[0].value = newValue;
});

watch(filterdays, (newValue) => {
  filters.value.days.constraints[0].value = newValue;
});

initFilters();

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
setInterval(() => {
  loading.value=false
  content.value=true
}, 500);

    filterLastWeek();
    getdata();
  });
  
  const filterLastWeek = async() => {
    activeFilter.value = 'week';
  
    try {
  
      const res = await fetch('/amounttable.json');
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
      const data = await res.json();
      investamount.value=data[0].week.investamount
      currentvalue.value=data[0].week.currentvalue
      overallgain.value=data[0].week.overallgain
      todaygain.value=data[0].week.todaygain

    } catch (error) {
      console.error("Error:", error.message);
    }

  

    setDateRange(6);
  };
  
  const filterLast15Days = async() => {
   
    activeFilter.value = '15days';
    try {
     
      const res = await fetch('/amounttable.json');
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
      const data = await res.json();
      investamount.value=data[1].day_15.investamount
      currentvalue.value=data[1].day_15.currentvalue
      overallgain.value=data[1].day_15.overallgain
      todaygain.value=data[1].day_15.todaygain

    } catch (error) {
      console.error("Error:", error.message);
    }
    
    setDateRange(14);
  };
  
  const filterLastMonth = async() => {
    activeFilter.value = 'month';
    try {
      
      const res = await fetch('/amounttable.json');
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
      const data = await res.json();
      investamount.value=data[2].month.investamount
      currentvalue.value=data[2].month.currentvalue
      overallgain.value=data[2].month.overallgain
      todaygain.value=data[2].month.todaygain

    } catch (error) {
      console.error("Error:", error.message);
    }
    setDateRange(30);
  };
  
  const filterLast3Months = async() => {
    activeFilter.value = '3months';
    try {
      
      const res = await fetch('/amounttable.json');
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
      const data = await res.json();
      investamount.value=data[3].month_3.investamount
      currentvalue.value=data[3].month_3.currentvalue
      overallgain.value=data[3].month_3.overallgain
      todaygain.value=data[3].month_3.todaygain

    } catch (error) {
      console.error("Error:", error.message);
    }
    setDateRange(90);
  };
  
  const setDateRange = (days) => {
    const today = new Date();
    const startDate = new Date();
    startDate.setDate(today.getDate() - days);
    dates.value = [startDate.toISOString().split('T')[0], today.toISOString().split('T')[0]];
  };
  
  const handleDateChange = (newDates) => {
    activeFilter.value = 'customs';
    dates.value = newDates;
  };
  
  const customs=()=>{
    activeFilter.value = 'customs';
    visible.value=true

  }
  const filteredCustomers = computed(() => {
    if (!dates.value || dates.value.length !== 2) {
      return customers.value;
    }
  
    const startDate = new Date(dates.value[0]);
    const endDate = new Date(dates.value[1]);
    endDate.setHours(23, 59, 59, 999);
  
    return customers.value.filter(customer => {
      const customerDate = new Date(customer.date);
      return customerDate >= startDate && customerDate <= endDate;
    });
  });

  const columns = ref([
  { field: 'stockname', header: 'Stockname' },
  { field: 'quantity', header: 'Quantity' },
  { field: 'avgprice', header: 'Avgprice' },
  { field: 'ltp', header: 'Ltp' },
  { field: 'invamt', header: 'Invamt' },
  { field: 'mktval', header: 'Mktval' },
  { field: 'overall', header: 'Overall' },
  { field: 'days', header: 'Days' },
  { field: 'date', header: 'Date' },
  { field: 'action', header: 'Action' },
]);

// Initially select all columns except 'ltp', 'mktval', and 'date'
const selectedColumns = ref(columns.value.filter(col => !['ltp', 'mktval', 'date'].includes(col.field)));
const visibleColumns = ref(selectedColumns.value.map(col => col.field)); // Tracks visibility
const showReset = ref(true); // Ensure reset is visible as some columns are unchecked initially

const updateVisibleColumns = () => {
  visibleColumns.value = selectedColumns.value.map(col => col.field);
  showReset.value = selectedColumns.value.length < columns.value.length; // Show Reset only when some columns are unchecked
};

const resetColumns = () => {
  selectedColumns.value = columns.value.slice(); // Reset to all columns selected
  updateVisibleColumns(); // Ensure UI updates
};

watch(selectedColumns, updateVisibleColumns, { deep: true });


  const dt = ref();

const exportCSV = () => {
    dt.value.exportCSV();
};
const stockname=ref('')
const dateval=ref('')
const quant=ref('')
const avg=ref('')
const ltp=ref('')
const invamt=ref('')
const mktval=ref('')
const overall=ref('')
const days=ref('')
const rightcanva =(dataval)=>{
    visibleRight.value=true
    stockname.value=dataval.stockname
    dateval.value=dataval.date
    quant.value=dataval.quantity
    avg.value=dataval.avgprice
    ltp.value=dataval.ltp
    invamt.value=dataval.invamt
    mktval.value=dataval.mktval
    overall.value=dataval.overall
    days.value=dataval.days
}

const proceedfun=async()=>{
  try {
      const res = await fetch('/proceed.json');
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
      const data = await res.json();
      toast.add({ severity: 'success', summary: 'Success Message', detail: data[0].proceed, life: 3000 });
    } catch (error) {
      console.error("Error:", error.message);
    }
  
    
}

const cancelfun=async()=>{
  
  try {
      const res = await fetch('/proceed.json');
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
      const data = await res.json();
      toast.add({ severity: 'error', summary: 'Cancel Message', detail: data[0].cancel, life: 3000 });
    } catch (error) {
      console.error("Error:", error.message);
    }
}
  </script>
  <style>

</style>
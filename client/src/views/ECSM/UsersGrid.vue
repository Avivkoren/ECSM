<template>
  <div class="UsersGrid">
    <ejs-grid  ref='LiorGrid' height=480  locale='he-IL' :allowFiltering='true' :allowSorting='true' :filterSettings='filterOptions'  :created='created' :dataSource="dataSource" :toolbar='toolbar'  :editSettings='editSettings' :toolbarClick='toolbarClick'  :allowExcelExport='true' > 
      <e-columns>
        <e-column field='ID'  headerText='ID' textAlign='Right' width=60 :allowEditing ='false' :isPrimaryKey='true'></e-column>
        <e-column field='First' headerText='שם פרטי' textAlign='Right' width=100></e-column>
        <e-column field='Last' headerText='שם משפחה' textAlign='Right' width=120></e-column>
        <e-column field='Team' headerText='צוות' textAlign='Right' width=100 :visible='false'></e-column>
        <e-column field='User' headerText='שם משתמש' textAlign='Left' width=120></e-column>
        <e-column field='PassWord' headerText='סיסמא' textAlign='Left' width=100></e-column> 
        <e-column field='Email' headerText='מייל' textAlign='Left' width=150></e-column> 
        <e-column field='Phone' headerText='טלפון' textAlign='Left' width=100   ></e-column> 
       
      </e-columns>
    </ejs-grid>
  </div>
</template>

<script lang="ts">
    import Vue from 'vue';
    import { L10n, setCulture } from '@syncfusion/ej2-base';
    import { GridPlugin, Filter, Sort, Edit, Toolbar,ExcelExport } from '@syncfusion/ej2-vue-grids';
    import { DataManager, WebApiAdaptor,RemoteSaveAdaptor } from "@syncfusion/ej2-data";
    import UsersData from '../../services/GetDataServices';
    import HebConf from './GridHebConfig.js';
    import ServerConfig from '../../ServerConfig';

    setCulture('he-IL');
    L10n.load(HebConf);

    Vue.use(GridPlugin);

export default Vue.extend({
      data: ()=>{

return {
                dataSource: new DataManager({
                  json: [],
                  adaptor: new RemoteSaveAdaptor,
                  insertUrl: ServerConfig.UsersAPI + 'InsertUser',
                  updateUrl: ServerConfig.UsersAPI + 'UpdateUser',
                  removeUrl: ServerConfig.UsersAPI + 'DeleteUser',
                }), 
                filterOptions: {
                  type: 'CheckBox'
                },
                toolbar: ['Add', 'Edit', 'Delete', 'Update', 'Cancel'],
                editSettings: { allowEditing: true, allowAdding: true, allowDeleting: true, showDeleteConfirmDialog: true },
                
              };
      },
      provide: {
        grid: [Sort,Filter,Edit, Toolbar]       
      },
      methods:{
            created() { 
              var gridOj =this.$refs.LiorGrid;  
              UsersData.GetUsersData(gridOj);
            },
      }
    } );
      
 
</script>

<style>
    @import '../../../node_modules/@syncfusion/ej2-base/styles/material.css'; 
    @import '../../../node_modules/@syncfusion/ej2-buttons/styles/material.css'; 
    @import '../../../node_modules/@syncfusion/ej2-calendars/styles/material.css'; 
    @import '../../../node_modules/@syncfusion/ej2-dropdowns/styles/material.css'; 
    @import '../../../node_modules/@syncfusion/ej2-inputs/styles/material.css'; 
    @import '../../../node_modules/@syncfusion/ej2-navigations/styles/material.css'; 
    @import '../../../node_modules/@syncfusion/ej2-popups/styles/material.css'; 
    @import '../../../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css'; 
    @import "../../../node_modules/@syncfusion/ej2-vue-grids/styles/material.css"; 
</style>


### 默认选择到年月

    $("#datepicker").datepicker( {
        format: "yyyy-mm",
        viewMode: "months", 
        minViewMode: "months"
    });

For version 1.2.0 and newer, viewMode has changed to startView, so use:

    $('#datepicker').datepicker({
        format:'yyyy-mm',
        startView:'months',
        minViewMode:'months',
    })
    
data-provide="datepicker" data-date-start-date="+1d" 起始时间是当前时间+1天

data-provide="datepicker" data-date-end-date="+1M" 起始时间是当前时间的+1月



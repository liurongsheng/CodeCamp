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
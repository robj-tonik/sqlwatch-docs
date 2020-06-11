# Using Apply instead of Join

You will notice a lot of the dimension views use `OUTER APPLY` instead of the `LEFT JOIN` . Outer apply is significantly slower than left join but it only "triggers" when columns are being selected. If the select statement does not include columns from the apply statement, the apply is not being run at all. This is different to a join behaviour where the join is always executed regardless what columns are being selected.

The dimension views have been optimised for Power BI and the APPLY does not fire when used via Power BI. However, as the application is universal, additional columns where included in the views to make manual queries easier. This approach gives significant performance boost in a "normal" operation but with the added benefit of flexibility when required.  

{% hint style="info" %}
If you are querying the views manually and need to return columns from the apply routine, please make sure you have a WHERE clause to limit the number of rows/iterations.
{% endhint %}




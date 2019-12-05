# Power BI Load Errors

You may experience errors during data load into Power BI that may look similar to the below:

![](../.gitbook/assets/image%20%2865%29.png)

This is caused by Privacy Settings in Power BI which you will have to disable:

![](../.gitbook/assets/image%20%2824%29.png)

When Power BI loads data it makes sure that data from different sources \(or tables\) does not get mixed up which, in some systems, could cause privacy issues. Since we are joining different SQLWATCH tables during the load \(time dimensions and facts\) this error will likely always pop up. I do not know any other solution at this point, if you do, please get in touch.

{% hint style="info" %}
Note no other sources or tables are being loaded into SQLWATCH. All data comes from the SQLWATCH database and queries are not being sent anywhere.
{% endhint %}


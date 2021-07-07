# Jinja templating engine<a name="ag-jinja"></a>

AWS Proton uses the [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) templating engine to match schema customization parameters with values it receives when you use an infrastructure template to create an AWS Proton resource\.

**Requirements**
+ Use AWS Proton name\-spaces\.
+ Use double moustache brackets surrounded by single quotation marks to identify them in your infrastructure template files\.

**Example**

```
port: '{{ service_instance.inputs.port }}'
```
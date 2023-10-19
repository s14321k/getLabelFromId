# getLabelFromId

```
function getPt()
{
   
    var form = document.getElementById('updateTable');
    console.log(form);


    var inputNodes = form.getElementsByTagName('*');
    var map = new Map();
    for(var i = 0; i < inputNodes.length; ++i)
    {
         var inputNode1 = inputNodes[i];
         var inputVale = inputNode1.value;
//console.log("inputVale== "+inputVale);
         var inputName = inputNode1.name;
//console.log("inputName== "+inputName);
         var innerHTMl = inputNode1.innerHTML;
//console.log("innerHTMl== "+innerHTMl);
    var innerTexT = inputNode1.innerText;
console.log("innerTexT== "+innerTexT);
         map.set(inputName,inputVale);
    }
    for (const [key, value] of map.entries())
    {
         console.log("Map Values :: "+ `${key} = ${value}`);
    }

    var formData = new FormData(form);
    console.log(formData);
    var objFormEntries = Object.fromEntries(formData);
    console.log("objFormEntries= "+objFormEntries);
    var strJson = JSON.stringify(Object.fromEntries(formData));
    console.log("strJson= "+strJson);
    var modOb = Object.keys(objFormEntries).reduce(function(p, c)
    {
        return p.concat([encodeURIComponent(c) + "=" + encodeURIComponent(objFormEntries[c])]);
    }, []);
   
    console.log("modOb= "+modOb);
    var urlEncodedData = modOb.join("&").replace(/%20/g, "+");  
    console.log("urlEncodedData= "+urlEncodedData);
}
```

https://youtu.be/mPPhcU7oWDU

https://www.baeldung.com/spring-jdbctemplate-in-list

https://stackoverflow.com/q/10606229

https://www.baeldung.com/sql-injection

https://www.tabnine.com/code/java/methods/org.springframework.jdbc.core.namedparam.NamedParameterJdbcTemplate/queryForObject

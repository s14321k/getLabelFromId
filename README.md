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


```


function getPt2()
{
    var jsonObj ={};
    var form = document.getElementById('getJson');
    var inputNodes = form.querySelectorAll("mat-label,table,mat-expansion-panel, thead, tbody, th, tr, td,select, label, h4, mat-card-subtitle, button, div:not(.mat-select-value):not(.mat-paginator-range-actions):not(.mat-paginator-range-label):not(i)");
    /*var inputNodes = form.querySelectorAll("span");
    var inputNodes = form.querySelectorAll('*:not(input):not(select)');
    var inputNodes = form.getElementsByTagName('*');
   
    var filteredNodes = [];
    for (var i = 0; i < inputNodes.length; i++)
    {
        var currentNode = inputNodes[i];
        if (!currentNode.closest('.mat-paginator-range-label'))
        {
            filteredNodes.push(currentNode);
        }
        else
        {
            console.log("got it");
        }
    }*/
   
    for(var i = 0; i < inputNodes.length; i++)
    {
        var inputNode1 = inputNodes[i];
        var outerTexT = inputNode1.outerText;
        const relsArray = outerTexT.split(/\r\n|\n|\r/);
                /*space (' ')
                tab (\t)
                carriage return (\r)
                line feed (\n), and
                vertical tab (\v)*/
       
        for(var j=0; j < relsArray.length; j++)
        {
            const conVal = relsArray[j];
            var firstRep = conVal.replace("#", "");
            if(firstRep===undefined || firstRep.indexOf("\t") !== -1 || firstRep === "" || firstRep === null || firstRep.match(/^ *$/) !== null || firstRep.trim() === '' || firstRep === "print")
            {
                continue;
            }
            else
            {
                let key = capitalizeAfterSpace(conVal);
                for(var k=0; k <key.length; k++)
                {
                    if(containsWhitespace(key))
                    {
                    key = key.trim();
                    key = replaceChars(key);
                    }
                    else
                    {
                    continue;
                    }
                }
               
                var value = conVal.charAt(0).toUpperCase() + relsArray[j].slice(1);
                key = key.charAt(0).toLowerCase() + key.slice(1);
               
                if(!jsonObj.hasOwnProperty(key))
                {
                    key = replaceChars(key);
                    value = replaceChars(value);
                    jsonObj[key] = value;
                }
            }
        }
        var lastVal = JSON.stringify(jsonObj);
        console.log(lastVal);
    }
}


function containsWhitespace(str)
{
    return /\s/.test(str);
}


function replaceChars(keyValus)
{
    keyValus = allReplace(keyValus,
        {
            'navigate_beforeBack':'back',
            'Navigate_beforeBack' : "Back",
            'nextnavigate_next' : 'next',
            'Nextnavigate_next' : 'Next',
            'nextNavigate_next' : 'next',
            'Next navigate_next' : 'Next',
            'add_circle' : '',
            'Add_circle' : '',
            'descriptionUploadFiles' : 'uploadFiles',
            'Description Upload Files' : 'Upload Files',
            '\\#' : '',
            '\\*' : ''
        });
   
    // keyValus = keyValus.replace("navigate_beforeBack", "back");
   
    return keyValus;
}

function allReplace(str, obj)
{
    for (const x in obj)
    {
        if (x.search('[a-z]\\.\\+\\*\\#') != -1)
        {
            console.log(x);
        }
        str = str.replace(new RegExp(x, 'g'), obj[x]);
    }
    return str;
}


function capitalizeAfterSpace(conVal)
{
    let key = "";
    let capitalizeNext = false;

    for (let i = 0; i < conVal.length; i++)
    {
        const char = conVal[i];
        if (char === " ")
        {
            capitalizeNext = true;
        }
        else if (capitalizeNext)
        {
            key += char.toUpperCase();
            capitalizeNext = false;
        }
        else
        {
            key += char;
        }
    }
    return key;
}


```
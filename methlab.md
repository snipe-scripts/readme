-- Add to shared.lua

```lua
    ["meth_baggy"]            =     {["name"] = "meth_baggy",            ["label"] = "Meth",                    ["weight"] = 200,         ["type"] = "item",         ["image"] = "meth_bag.png",             ["unique"] = true,         ["useable"] = false,     ["shouldClose"] = true,           ["combinable"] = nil,   ["description"] = "Meth Baggy"},
    ["meth_powder"]            =     {["name"] = "meth_powder",            ["label"] = "Meth Powder",            ["weight"] = 1000,         ["type"] = "item",         ["image"] = "meth_powder.png",             ["unique"] = true,         ["useable"] = false,     ["shouldClose"] = true,           ["combinable"] = nil,   ["description"] = "Powder of Meth"},
    ["sodium_benzoate"]        =     {["name"] = "sodium_benzoate",        ["label"] = "Sodium Benzoate",        ["weight"] = 1000,         ["type"] = "item",         ["image"] = "sodium_benzoate.png",         ["unique"] = false,     ["useable"] = false,     ["shouldClose"] = true,           ["combinable"] = nil,   ["description"] = "A alkaline solution used in Meth Labs"},
    ["propylene_glycol"]    =     {["name"] = "propylene_glycol",        ["label"] = "Propylene Glycol",        ["weight"] = 1000,         ["type"] = "item",         ["image"] = "propylene_glycol.png",     ["unique"] = false,     ["useable"] = false,     ["shouldClose"] = true,           ["combinable"] = nil,   ["description"] = "A acidic solution used in Meth Labs"},
```


-- Add to inventory/html/app.js

Look for  ```function FormatItemInfo```

Add this two else if statements below labkey (labkey part already exists)

```js
else if (itemData.name == "labkey") {
    $(".item-info-title").html("<p>" + itemData.label + "</p>");
    $(".item-info-description").html("<p>Lab: " + itemData.info.lab + "</p>");
} else if (itemData.name == "meth_baggy") {
    $(".item-info-title").html('<p>'+itemData.label+'</p>')
    $(".item-info-description").html('<p><b>QI - </b>'+itemData.info.qualityIndex+'%</p><br/>');
} else if (itemData.name == "meth_powder") {
    $(".item-info-title").html('<p>'+itemData.label+'</p>')
    $(".item-info-description").html('<p><b>QI - </b>'+itemData.info.qualityIndex+'%</p><br/>');
}
```

If you want to spawn the items like meth_baggy or meth_powder, make sure to do following changes in qb-inventory/server/main.lua

Look for : 
`QBCore.Commands.Add("giveitem", "Give An Item (Admin Only)", {{name="id", help="Player ID"},{name="item", help="Name of the item (not a label)"}, {name="amount", help="Amount of items"}}, true, function(source, args)`

and add the following 4 lines. This will give metadata to the items so you dont get errors while processing or breaking the items into smaller items

```lua
elseif itemData["name"] == "meth_baggy" then
    info.qualityIndex = math.random(70,100)
elseif itemData["name"] == "meth_powder" then
    info.qualityIndex = math.random(70,100)
```


-- Shells 

Once you download shells from Max Creations, make sure to use one of them and ensure it before the methlab script.

-- Add the images in inventory/html/images
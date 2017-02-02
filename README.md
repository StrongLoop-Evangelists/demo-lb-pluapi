#PLUAPI

### did you ever wish you had an API for those little stickers on fruit & veg at the supermarket? Now you can.

## datasource
This data is from the International Federation of Produce Standards. You can download the data [here](http://www.ifpsglobal.com/Identification/PLU-Codes/PLU-codes-Search). 

Thanks to [Jeremy Singer-Vine](https://twitter.com/jsvine)'s wonderful [Data Is Plural newsletter](https://tinyletter.com/data-is-plural) for the original link to this dataset.


##setup

1. `npm install –g loopback-cli`
2. `lb -l` for commands
3. `lb app`	
4. `lb datasource` (see below)
4. `lb model` (see below)

##datasource
* make sure you have a local Mongo running
* `lb datasource`
* name your datasource 'mongo'
* select the 'MongoDB (supported by StrongLoop)' connector
* enter `mongodb://localhost:27017/test` as your connection string
* skip the `host, port, user, password`, and `database` entries
* answer yes to `Install loopback-connector-mongodb@^1.4?`

##model
Here's a sample record of PLU Codes data: 

```json
    {
    "PLU": 3001,
    "CATEGORY": "",
    "COMMODITY": "APPLES",
    "VARIETY": "Aurora/Southern Rose",
    "ADDITIONAL VARIETY INFO": "",
    "SIZE": "Small",
    "NA SIZE": "100 size and smaller",
    "ROW SIZE": "Average Fruit Weight = less than 205g",
    "RESTRICTIONS": "",
    "NOTES": "",
    "AKA": "",
    "TRADEMARK": "",
    "BOTANICAL NAME": "Malus pumila",
    "REVISION DATE": "2016-04-07 23:21:26",
    "DATE ADDED": "1999-12-31 00:00:00",
    "GPC": 10005900,
    "IMAGE": ""
  }
```
And here's how the model looks after using the `lb model` dialog (NOTE! key names are case-sensitive):

```json
{
    "PLU": {
      "type": "number",
      "required": true,
      "id": true
    },
    "category": {
      "type": "string"
    },
    "commodity": {
      "type": "string"
    },
    "variety": {
      "type": "string"
    },
    "varietyInfo": {
      "type": "string"
    },
    "size": {
      "type": "string"
    },
    "NASize": {
      "type": "string"
    },
    "rowSize": {
      "type": "string"
    },
    "restrictions": {
      "type": "string"
    },
    "AKA": {
      "type": "string"
    },
    "notes": {
      "type": "string"
    },
    "trademark": {
      "type": "string"
    },
    "botanicalName": {
      "type": "string"
    },
    "revisionDate": {
      "type": "date"
    },
    "dateAdded": {
      "type": "date"
    },
    "GPC": {
      "type": "number",
      "required": true
    },
    "image": {
      "type": "string"
    }
  }
```
###more notes on models:
* if you set ` "idInjection": true` and don't have an explicit `"id": true` on any property, Loopback will add an id property for you and add an id to any record POSTed.
* for this example, `idInjection` is set to `false` and `PLU` is given a property of `"id": true`. This will make `PLU` the id property for Mongo and for endpoints such as `http://0.0.0.0:3000/api/PLUs/3001` (where `3001` is the PLU code). 



##run
* for debug mode: `DEBUG=loopback:connector:mongodb node .`
* otherwise: `node .`
* with nodemon: 
`npm install -D nodemon` then `DEBUG=loopback:connector:mongodb nodemon .` or `nodemon .`


##interact
* to open the Explorer: `http://0.0.0.0:3000/explorer`

##presented at
* DonutJS 31 Jan 2017 [slides](http://www.slideshare.net/emckean/mckeanpluapidonutjs)


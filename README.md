# aps-da4acad-dgn2dwg2pdf

In this repo I'm sharing [Design Automation](https://aps.autodesk.com/developer/overview/design-automation-api) activities and workitems payload that you can use to cover two steps:

1. Convert a dgn file to dwg
2. Convert a dwg to pdf

You can check the workflows in the video below:

### [Video Here](https://www.youtube.com/watch?v=XOpjI1xezTw)

Kudos to Madhukar for all the help with this :)
## DGN TO DWG
Activity below:
```json
{
	"id": "Your activity name",
	"commandLine": [
		"$(engine.path)\\accoreconsole.exe /s $(settings[script].path)"
	],
	"parameters": {
		"inputdgn": {
			"verb": "get",
			"description": "input DGN file",
			"required": true,
			"localName": "input.dgn"
		},
		"result": {
			"verb": "put",
			"description": "resultdrawing",
			"required": true,
			"localName": "result.dwg"
		}
	},
	"engine": "Autodesk.AutoCAD+25_0",
	"description": "DGNtoDWG",
	"settings": {
		"script": "(command\"-dgnimport\" \"input.dgn\" \"\" \"\" \"\" \"save\" \"result.dwg\")\n"
	}
}
```
You must use the engine Autodesk.AutoCAD+25_0

Workitem below:

```json
{
  "activityId": "Your activity fully qualified id",
  "arguments": {
    "inputdgn": {
      "url": "urn:adsk.objects:os.object:<<bucketkey>>/somedgnfile.dgn",
      "verb": "get",
      "Headers": {
        "Authorization": "Bearer yourtokenhere"
      }
    },
    "result": {
      "verb": "put",
      "url": "urn:adsk.objects:os.object:<<bucketkey>>/somedgnfile.dwg",
      "Headers": {
        "Authorization": "Bearer yourtokenhere"
      }
    },
    "onProgress": {
      "verb": "post",
      "url": "yourcallbackurl",
      "Headers": {
        "Content-Type": "application/json"
      }
    },
    "onComplete": {
      "verb": "post",
      "url": "yourcallbackurl",
      "Headers": {
        "Content-Type": "application/json"
      }
    }
  }
}
```

## DWG to PDF 

Simply use the shared activity `AutoCAD.PlotToPDF+prod`

Workitem below:
```json
{
  "activityId": "AutoCAD.PlotToPDF+prod",
  "arguments": {
    "HostDwg": {
      "url": "urn:adsk.objects:os.object:<<bucketkey>>/somedgnfile.dwg",
      "verb": "get",
      "Headers": {
        "Authorization": "Bearer yourtokenhere"
      }
    },
    "Result": {
      "verb": "put",
      "url": "urn:adsk.objects:os.object:<<bucketkey>>/somedgnfile.pdf",
      "Headers": {
        "Authorization": "Bearer yourtokenhere"
      }
    },
    "onProgress": {
      "verb": "post",
      "url": "yourcallbackurl",
      "Headers": {
        "Content-Type": "application/json"
      }
    },
    "onComplete": {
      "verb": "post",
      "url": "yourcallbackurl",
      "Headers": {
        "Content-Type": "application/json"
      }
    }
  }
}
```

## License

This sample is licensed under the terms of the [MIT License](http://opensource.org/licenses/MIT). Please see the [LICENSE](LICENSE) file for full details.

## Written by

João Martins [in/jpornelas](https://linkedin.com/in/jpornelas)

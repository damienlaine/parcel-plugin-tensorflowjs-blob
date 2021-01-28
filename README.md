# parcel-plugin-tensorflow-blob
Inline TensorFlowJS models in your app bundle. Simply import weight manifest .bin file and get associated model.json as a blob URL

Ideal for delivering your machine-learning inference application as a single .js for script tag injection 

# Usage
Install the plugin :

```bash
npm i parcel-plugin-tensorflow-blob
```

## Import a single model and load it in TensorFlowJS

You might want to have this kind of path in your project:

```bash
.
|-- model
|   |-- group1-shard1of1.bin
|   `-- model.json

```

```js

import modelWeightManifest from "model/group1-shard1of1.bin"
const modelTopologyBlobURL = modelWeightManifest.blobModelPath()

mySuperModel = await tf.loadLayersModel(modelTopologyBlobURL)
```

## Import multiple models at once

```bash
.
|-- models
|   |-- model1
|   |   |-- group1-shard1of1.bin
|   |   `-- model.json
|   |-- model2
|   |   |-- group1-shard1of1.bin
|   |   `-- model.json
|   `-- model3
|       |-- group1-shard1of1.bin
|       `-- model.json

```

use globs :

```js

import modelWeightManifests from "models/**/*.bin"

```

## How does it works ?

This script embbeds bin weight files as Bas64 encoded string and model.json as string at bundling time. It wraps them in a function (__blobModelPath__). Calling this function on imported .bin asset:
- Decodes the base64 string
- Constructs a blob object for the decoded bin and a blob URL for it
- Edits model.json with the weight manifest blob
- Constructs a blob object for the model.json
- Returns the model.json's blob URL, which is obviously related to

# Fits your needs ?

Glad ! I hope this plugin helps you focus on building models and evaporates all the burden of building distribuable TensorFlowJS apps or libraries

If not, look for __IOHandler__ documentation in TensorFlowJS. SPOILER : It's quirky and motivated me to write this parcel plugin ;)

You might also contribute to this project.
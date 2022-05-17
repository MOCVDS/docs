# Some Outlines Draft

The example that I will use here is of an API and model that I have created and use to predict birds visiting birdfeeders.

- Model: [https://github.com/bird-feeder/BirdFSD-YOLOv5](https://github.com/bird-feeder/BirdFSD-YOLOv5)
- API: [https://github.com/bird-feeder/BirdFSD-YOLOv5-API](https://github.com/bird-feeder/BirdFSD-YOLOv5-API) (recently developed, no documentation)

## Example Result

### Raw input
file_name: `demo.png`

![demo.png](https://d.aibird.me/8890c6c6.png)


### API call

```sh
curl -X POST "http://127.0.0.1:8000/predict" -F file="@demo.png"
```

### API response

```json
{
    "results": {
        "input_image": {
            "name": "demo.png",
            "hash": "6c9ed1b20b82112e057ac2ece74795ec"
        },
        "labeled_image_url": "https://api-s3.aibird.me/api/14705b1a661a.jpg",
        "predictions": {
            "0": {
                "confidence": 0.9704,
                "name": "Brown-headed cowbird (Molothrus ater)",
                "bbox": {
                    "xmin": 0.2905663549900055,
                    "ymin": 0.5605813264846802,
                    "xmax": 0.5082285404205322,
                    "ymax": 0.8753182888031006
                },
                "species_info": {
                    "gbif": {
                        "usageKey": 2484391,
                        "scientificName": "Molothrus ater (Boddaert, 1783)",
                        "canonicalName": "Molothrus ater",
                        "rank": "SPECIES",
                        "kingdom": "Animalia",
                        "phylum": "Chordata",
                        "order": "Passeriformes",
                        "family": "Icteridae",
                        "genus": "Molothrus",
                        "species": "Molothrus ater",
                        "synonym": false,
                        "class": "Aves"
                    }
                }
            }
        },
        "model": {
            "name": "BirdFSD-YOLOv5",
            "version": "1.0.0-alpha.4",
            "page": "https://github.com/bird-feeder/BirdFSD-YOLOv5/releases/tag/BirdFSD-YOLOv5-v1.0.0-alpha.4"
        }
    }
}
```

![resp](https://api-s3.aibird.me/api/14705b1a661a.jpg)

### *Results* metdata by priority

#### High

- Model name and version
- confidence/accuracy/loss (i.e., model performance score)

#### Medium
- bbox
- key/id/url/dict of the species that can be linked to an established database (e.g., `gbif`).


#### Accessing the model in the API response

```sh
curl -X GET "http://127.0.0.1:8000/model" -F version="1.0.0-alpha.4"
```

##### API response

*ps: ignore the fact that the names in this example are common names.*

```json
{
    "name": "BirdFSD-YOLOv5",
    "version": "1.0.0-alpha.4",
    "architecture": "yolov5",
    "classes": {
        "American Goldfinch": 118,
        "Brown-headed Cowbird": 186,
        "Carolina Chickadee": 324,
        "Chipping Sparrow": 1084,
        "Downy Woodpecker": 114,
        "Hermit Thrush": 141,
        "House Finch": 566,
        "Northern Cardinal": 547,
        "Song Sparrow": 53,
        "Spotted/Eastern Towhee (Rufous-sided Towhee)": 110,
        "Tufted Titmouse": 418,
        "White-throated Sparrow": 32,
        "Yellow-rumped Warbler": 404,
        "squirrels": 248
    },
    "metrics": {
        "val/box_loss": 0.014154575765132904,
        "metrics/precision": 0.9508796149755222,
        "_step": 300,
        "train/box_loss": 0.006580885499715805,
        "train/cls_loss": 0.0006521922769024968,
        "metrics/mAP_0.5": 0.9827705006373556,
        "metrics/mAP_0.5:0.95": 0.8677826381209933,
        "x/lr2": 0.00016600000000000043,
        "metrics/recall": 0.9907824859847648,
        "_runtime": 71964,
        "val/obj_loss": 0.006690541747957468,
        "best/precision": 0.9508909511302966,
        "x/lr0": 0.00016600000000000043
    },
    "added_on": "2022-05-07 03:55:22.842000",
    "trained_on": "2022-05-06 00:00:00",
    "wandb_run_path": "biodiv/train/808p95Vj",
    "number_of_classes": 14,
    "number_of_annotations": 4345,
    "train_config": {
        "cfg": "",
        "hyp": {
            "box": 0.05,
            "cls": 0.5,
            "lr0": 0.01,
            "lrf": 0.01,
            "obj": 1,
            "hsv_h": 0.015,
            "hsv_s": 0.7,
            "hsv_v": 0.4,
            "iou_t": 0.2,
            "mixup": 0,
            "scale": 0.5,
            "shear": 0,
            "cls_pw": 1,
            "fliplr": 0.5,
            "flipud": 0,
            "mosaic": 1,
            "obj_pw": 1,
            "degrees": 0,
            "anchor_t": 4,
            "fl_gamma": 0,
            "momentum": 0.937,
            "translate": 0.1,
            "copy_paste": 0,
            "perspective": 0,
            "weight_decay": 0.0005,
            "warmup_epochs": 3,
            "warmup_bias_lr": 0.1,
            "warmup_momentum": 0.8
        },
        "data": "dataset_config.yml",
        "name": "exp",
        "quad": false,
        "rect": false,
        "cache": null,
        "imgsz": 768,
        "noval": false,
        "bucket": "",
        "cos_lr": false,
        "device": "0",
        "entity": null,
        "epochs": 300,
        "evolve": null,
        "freeze": [
            0
        ],
        "nosave": false,
        "resume": false,
        "noplots": false,
        "project": "yolov5/runs/train",
        "sync_bn": false,
        "weights": "best.pt",
        "workers": 8,
        "exist_ok": false,
        "patience": 100,
        "save_dir": "yolov5/runs/train/exp5",
        "data_dict": {
            "nc": 14,
            "val": "dataset-YOLO/images/val",
            "path": "BirdFSD-YOLOv5/dataset-YOLO",
            "test": null,
            "names": [
                "American Goldfinch",
                "Brown-headed Cowbird",
                "Carolina Chickadee",
                "Chipping Sparrow",
                "Downy Woodpecker",
                "Hermit Thrush",
                "House Finch",
                "Northern Cardinal",
                "Song Sparrow",
                "Spotted/Eastern Towhee (Rufous-sided Towhee)",
                "Tufted Titmouse",
                "White-throated Sparrow",
                "Yellow-rumped Warbler",
                "squirrels"
            ],
            "train": "dataset-YOLO/images/train"
        },
        "optimizer": "SGD",
        "batch_size": 54,
        "local_rank": -1,
        "single_cls": false,
        "multi_scale": false,
        "save_period": 100,
        "dataset_name": "dataset-YOLO-05-06-2022_02.57.11.tar",
        "noautoanchor": false,
        "bbox_interval": -1,
        "image_weights": false,
        "artifact_alias": "latest",
        "upload_dataset": false,
        "label_smoothing": 0,
        "system_hardware": {
            "gpu_type": "Tesla V100-PCIE-32GB",
            "cpu_count": 40,
            "gpu_count": 1,
            "nvidia_driver_version": "470.103.01"
        },
        "base_ml_framework": {
            "CUDA": "10.2",
            "Torch": "1.11.0",
            "Python": "3.8.13",
            "Torchvision": "0.12.0"
        }
    },
    "page": "https://github.com/bird-feeder/BirdFSD-YOLOv5/releases/tag/BirdFSD-YOLOv5-v1.0.0-alpha.4"
}
```

### Model metadata in relation to the results, by priority

#### High

- Model name and version.
- A URL to the model's page (website, git repo, or publication).
- Classes names and the number of classes the model was trained on.
- Number of overall annotations and annotations per class.
- At least one standard overall score of the model performance based on the validation split.  -->  a list of standard tests that are accepted will be defined separately.
    1. If the model output includes object detection, then report the model's prediction score for the object detection task.
    2. If the model draws a bounding box, polygon, segmentation, etc., then report the model's score for the box/polygon/segmentation prediction task.
    3. If the model output includes class prediction (e.g., predicts the name of the species), then report the model's score for the class prediction score.

    *ps: if both `i` and `ii` exist, then reporting one is enough.*
- The name and URL of the dataset the model was trained on if the dataset is public. If the dataset is not public, a dataset name/id/key/source should be accepted as an alternative.


#### Medium
- Architecture (the name of the architecture the model is based on)
- Model performance per class.


#### Depends on whethere the model is public or private
- A URL to the pretrained weights file.


#### Example of model metadata that meets the minimum requirements:

*ps: ignore the fact that the names in this example are common names.*

```json
{
    "name": "BirdFSD-YOLOv5",
    "version": "1.0.0-alpha.4",
    "architecture": "yolov5",
    "classes": {
        "American Goldfinch": 118,
        "Brown-headed Cowbird": 186,
        "Carolina Chickadee": 324,
        "Chipping Sparrow": 1084,
        "Downy Woodpecker": 114,
        "Hermit Thrush": 141,
        "House Finch": 566,
        "Northern Cardinal": 547,
        "Song Sparrow": 53,
        "Spotted/Eastern Towhee (Rufous-sided Towhee)": 110,
        "Tufted Titmouse": 418,
        "White-throated Sparrow": 32,
        "Yellow-rumped Warbler": 404,
        "squirrels": 248
    },
    "metrics": {
        "val/obj_loss": 0.006690541747957468,
        "val/cls_loss": 0.0007224843720905483,
        "val/recall": 0.9907824859847648,
        "val/precision": 0.9508796149755222
    },
    "number_of_classes": 14,
    "number_of_annotations": 4345,
    "page": "https://github.com/bird-feeder/BirdFSD-YOLOv5/releases/tag/BirdFSD-YOLOv5-v1.0.0-alpha.4"
}
```

---

## TODO

- [ ]  A curated list of standard tests that are considered acceptable for reporting model performance.
- [ ]  A list with name and definiton of additional metrics that can be included on top of the standard metrics.
- [ ]  ... and more

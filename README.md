# Steps to run

Set kaggle to dual T4 gpu

Run notebook cell by cell as usual.

# Model analysis

## Model Chosen: The notebook uses yolov5 medium model with pre-trained weights for training.

## Training:
The model was trained for 50 epochs with a batch size of 64 and an image size of 640x640.
Training was performed on a dataset split into 80% for training and 20% for validation.
Specific hyperparameters were set for the training process, including learning rate, momentum, weight decay, and data augmentation parameters (HSV, degrees, translate, scale, shear, mosaic, mixup).
Distributed Data Parallelism was done  using 2 GPUs (--nproc_per_node 2 and --device 0,1).

## Inference:
Inference was run on the test dataset using the best.pt weights from the training experiment.
A confidence threshold of 0.3 and an IoU threshold of 0.5 were used for detection.
The results were saved with bounding box coordinates and confidence scores.

## Submission File Generation:
Predictions from the inference were processed to create a submission file.
Initially, multiple predictions per image were observed.
A filtering step was applied to keep only the highest confidence prediction per class per image.
Missing images (those in the test set without any predictions) were identified and added to the submission with random labels and zero confidence.
Finally, for images with multiple predictions after filtering, only the single highest confidence prediction per image was kept to match the expected submission format.
The final submission file was created by merging with the sample submission to align the 'id' column.

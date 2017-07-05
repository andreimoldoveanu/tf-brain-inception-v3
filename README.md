# tf-brain-inception-v3

Refer to https://codelabs.developers.google.com/codelabs/tensorflow-for-poets for detailed info.

Steps to retrain and test the net with your own images:

- Download images into a main directory with sub-directories for each category
  - mkdir <image_dir>
    - Example (it will create <image_dir> as "flower_photos"):
      - curl -O http://download.tensorflow.org/example_images/flower_photos.tgz
      - tar xzf flower_photos.tgz
- Create the directories
  - mkdir training_summaries
  - mkdir bottlenecks
  - mkdir -p training_summaries/basic
- tensorboard --logdir training_summaries &
- Fast retrain (low accuracy)
  - python retrain.py \
    --bottleneck_dir=bottlenecks \
    --how_many_training_steps=500 \
    --model_dir=inception \
    --summaries_dir=training_summaries/basic \
    --output_graph=retrained_graph.pb \
    --output_labels=retrained_labels.txt \
    --image_dir=<image_dir>
- Slow retrain (high accuracy) 
  - python /tensorflow/tensorflow/examples/image_retraining/retrain.py \
    --bottleneck_dir=bottlenecks \
    --model_dir=inception \
    --summaries_dir=training_summaries/long \
    --output_graph=retrained_graph.pb \
    --output_labels=retrained_labels.txt \
    --image_dir=flower_photos
- Test it
  - python label_image.py <new image to check> (Image shoud be different from the images used to train the net)

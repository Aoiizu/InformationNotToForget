# Title : Feline Body Condition Classification Using Mobile Deep Learning

## Tools to Consider 

**PyTorch**
More intuitive if you're doing a lot of research style experimenting.
Flaw: converting to mobile (via ONNX to TFLite, or PyTorch Mobile) is a bit more fiddly and has more compatibility issues.

### 2. Mobile Deployment
**TensorFlow Lite (TFLite)**
Built specifically for on device inference, small model size, works offline.
Flaw: some ops and layers aren't supported, so complex architectures sometimes need adjustments or quantization tuning, which can hurt accuracy.

**MediaPipe**
Great if you want built in pose or landmark detection, which is useful since cat body condition scoring often relies on key body points like ribs, waist, and spine.
Flaw: it's mainly tuned for human pose, so for cats you would have to train your own custom landmark model from scratch.

**ML Kit (Firebase)**
Simple to plug into an Android app.
Flaw: it mostly offers pre built models like face detection, text recognition, and barcodes. There's no cat specific model, so you would still need to bring your own custom model. ML Kit just hosts it for you.

### 3. App Framework
**Flutter**
One codebase for both Android and iOS, with decent camera plugin support.
Flaw: TFLite plugin integration can be inconsistent across versions and sometimes runs into native binding issues.

**React Native**
Flaw: ML integration here is generally less mature compared to plain native Android.

**Native Android (Kotlin) with TFLite**
Probably the most stable and direct path if you're using TFLite.
Flaw: you only get an Android version unless you build a separate iOS app too.

### 4. Dataset and Labeling
You'll most likely need to build your own dataset, meaning cat images labeled by body condition score, something like a 1 to 9 scale.
Flaw: this is usually the hardest part of the whole project. There's no big public "cat BCS" dataset out there, so you'll need vet reference charts, manual labeling, and probably some data augmentation to make up for a small sample size.

### 5. Annotation Tool
**Roboflow**
Easy web based labeling plus augmentation, and it exports straight to YOLO or TFLite formats.
Flaw: the free tier has limits, and exported formats sometimes need reformatting to fit your specific model.

## Core Project Flaws Worth Flagging in the Proposal
It's actually a good idea to name these honestly, since it shows you've thought through the limitations rather than ignoring them.

**No reliable ground truth**
Body condition scoring in real veterinary practice usually involves palpation, meaning actually feeling the ribs and fat under the fur, not just looking at the cat. So an image only ML approach has a real accuracy ceiling. Long haired or fluffy cats might look heavier than they actually are. It's worth mentioning this upfront as a scope limitation.

**Small or imbalanced dataset risk**
Most contributed cat photos will probably be of normal weight cats, with very few severely underweight examples, which can bias the model.

**No fixed reference scale in photos**
Without something like a ruler or a known sized object in frame, measuring actual size from a photo isn't very reliable. Only relative classification (like underweight, normal, overweight) tends to work well without that reference.

## Other Title Ideas (for reference)
PurrScan: A Mobile Application for Cat Weight Condition Assessment Using Computer Vision

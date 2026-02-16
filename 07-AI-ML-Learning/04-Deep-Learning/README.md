# 🧠 Deep Learning

Master Neural Networks, CNNs, RNNs, and modern deep learning with TensorFlow/PyTorch.

## 🎯 What is Deep Learning?

Deep Learning is a subset of Machine Learning using Neural Networks with multiple layers (deep networks).

**Why Deep Learning?**
- Excels at complex patterns (images, text, audio)
- Automatic feature extraction
- State-of-the-art performance on many tasks
- Powers modern AI (ChatGPT, Stable Diffusion, AlphaGo)

---

## 🧱 Neural Network Fundamentals

### Basic Architecture

```
Input Layer → Hidden Layers → Output Layer
```

### Key Components:

1. **Neurons**: Basic computational units
2. **Weights**: Parameters learned during training
3. **Activation Functions**: Add non-linearity
4. **Loss Function**: Measures error
5. **Optimizer**: Updates weights (gradient descent)

---

## 🔢 Simple Neural Network (PyTorch)

```python
import torch
import torch.nn as nn
import torch.optim as optim

# Define neural network
class SimpleNN(nn.Module):
    def __init__(self, input_size, hidden_size, output_size):
        super(SimpleNN, self).__init__()
        self.fc1 = nn.Linear(input_size, hidden_size)
        self.relu = nn.ReLU()
        self.fc2 = nn.Linear(hidden_size, output_size)
        self.sigmoid = nn.Sigmoid()

    def forward(self, x):
        x = self.fc1(x)
        x = self.relu(x)
        x = self.fc2(x)
        x = self.sigmoid(x)
        return x

# Create model
model = SimpleNN(input_size=10, hidden_size=20, output_size=1)

# Loss and optimizer
criterion = nn.BCELoss()  # Binary Cross Entropy
optimizer = optim.Adam(model.parameters(), lr=0.001)

# Training loop
for epoch in range(100):
    # Forward pass
    outputs = model(X_train)
    loss = criterion(outputs, y_train)

    # Backward pass
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()

    if (epoch + 1) % 10 == 0:
        print(f'Epoch [{epoch+1}/100], Loss: {loss.item():.4f}')
```

---

## 🖼️ Convolutional Neural Networks (CNNs)

**Use Case**: Image classification, object detection, computer vision

### CNN Architecture:
```
Input Image → Conv Layers → Pooling → Flatten → Dense Layers → Output
```

### Image Classification Example (TensorFlow/Keras):

```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers

# Load dataset (CIFAR-10)
(X_train, y_train), (X_test, y_test) = keras.datasets.cifar10.load_data()

# Normalize
X_train = X_train / 255.0
X_test = X_test / 255.0

# Build CNN
model = keras.Sequential([
    # Convolutional layers
    layers.Conv2D(32, (3, 3), activation='relu', input_shape=(32, 32, 3)),
    layers.MaxPooling2D((2, 2)),

    layers.Conv2D(64, (3, 3), activation='relu'),
    layers.MaxPooling2D((2, 2)),

    layers.Conv2D(64, (3, 3), activation='relu'),

    # Dense layers
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dropout(0.5),
    layers.Dense(10, activation='softmax')
])

# Compile
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

# Train
history = model.fit(
    X_train, y_train,
    epochs=10,
    batch_size=64,
    validation_split=0.2
)

# Evaluate
test_loss, test_acc = model.evaluate(X_test, y_test)
print(f'Test accuracy: {test_acc:.4f}')

# Save model
model.save('cnn_model.h5')
```

---

## 📝 Recurrent Neural Networks (RNNs)

**Use Case**: Sequential data (text, time series, speech)

### LSTM for Text Classification:

```python
from tensorflow.keras.layers import LSTM, Embedding, Dense
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences

# Sample text data
texts = ["I love this movie", "This is terrible", ...]
labels = [1, 0, ...]  # 1 = positive, 0 = negative

# Tokenize
tokenizer = Tokenizer(num_words=10000)
tokenizer.fit_on_texts(texts)
sequences = tokenizer.texts_to_sequences(texts)

# Pad sequences
X = pad_sequences(sequences, maxlen=100)

# Build LSTM model
model = keras.Sequential([
    Embedding(input_dim=10000, output_dim=128, input_length=100),
    LSTM(64, return_sequences=True),
    LSTM(32),
    Dense(1, activation='sigmoid')
])

model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])

# Train
model.fit(X, labels, epochs=10, batch_size=32, validation_split=0.2)
```

---

## 🔄 Transfer Learning

**Idea**: Use pre-trained models and fine-tune for your task

### Using Pre-trained Models:

```python
from tensorflow.keras.applications import ResNet50
from tensorflow.keras.applications.resnet50 import preprocess_input

# Load pre-trained ResNet50 (trained on ImageNet)
base_model = ResNet50(weights='imagenet', include_top=False, input_shape=(224, 224, 3))

# Freeze base model
base_model.trainable = False

# Add custom layers
model = keras.Sequential([
    base_model,
    layers.GlobalAveragePooling2D(),
    layers.Dense(256, activation='relu'),
    layers.Dropout(0.5),
    layers.Dense(num_classes, activation='softmax')
])

# Compile and train on your dataset
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
model.fit(X_train, y_train, epochs=10, validation_data=(X_val, y_val))
```

**Popular Pre-trained Models**:
- **Computer Vision**: ResNet, VGG, Inception, EfficientNet
- **NLP**: BERT, GPT, T5, RoBERTa (via Hugging Face)

---

## 🎨 Data Augmentation

Increase training data by transforming existing images:

```python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

# Data augmentation
datagen = ImageDataGenerator(
    rotation_range=20,
    width_shift_range=0.2,
    height_shift_range=0.2,
    horizontal_flip=True,
    zoom_range=0.2
)

# Fit on training data
datagen.fit(X_train)

# Train with augmented data
model.fit(datagen.flow(X_train, y_train, batch_size=32), epochs=50)
```

---

## 🛠️ Common Techniques

### 1. Regularization (Prevent Overfitting):

```python
# Dropout
layers.Dropout(0.5)

# L2 Regularization
layers.Dense(64, activation='relu', kernel_regularizer=keras.regularizers.l2(0.01))

# Batch Normalization
layers.BatchNormalization()
```

### 2. Callbacks:

```python
# Early stopping
early_stop = keras.callbacks.EarlyStopping(monitor='val_loss', patience=5)

# Model checkpoint (save best model)
checkpoint = keras.callbacks.ModelCheckpoint('best_model.h5', save_best_only=True)

# Learning rate scheduling
lr_schedule = keras.callbacks.ReduceLROnPlateau(monitor='val_loss', factor=0.5, patience=3)

# Train with callbacks
model.fit(X_train, y_train, epochs=100, callbacks=[early_stop, checkpoint, lr_schedule])
```

---

## 🏋️ Practice Projects

### Project 1: Image Classification
- **Dataset**: CIFAR-10 or MNIST
- **Goal**: Classify images into categories
- **Techniques**: CNN, Data Augmentation, Transfer Learning

### Project 2: Sentiment Analysis
- **Dataset**: IMDB Reviews
- **Goal**: Classify text as positive/negative
- **Techniques**: LSTM, Word Embeddings, Pre-trained models

### Project 3: Object Detection
- **Dataset**: COCO or Pascal VOC
- **Goal**: Detect objects in images
- **Techniques**: YOLO, Faster R-CNN, Transfer Learning

### Project 4: Time Series Forecasting
- **Dataset**: Stock prices or weather data
- **Goal**: Predict future values
- **Techniques**: LSTM, GRU, Attention mechanisms

---

## 📚 TensorFlow vs PyTorch

| Feature | TensorFlow | PyTorch |
|---------|-----------|---------|
| **Learning Curve** | Moderate | Easier |
| **Production** | Better (TF Serving) | Improving |
| **Research** | Good | Preferred |
| **Community** | Large | Growing fast |
| **Mobile** | TensorFlow Lite | PyTorch Mobile |

**Recommendation**: Learn PyTorch first (easier), then TensorFlow for production.

---

## 🔗 Resources

### Courses:
- **Fast.ai Practical Deep Learning** - Best hands-on course
- **Deep Learning Specialization (Andrew Ng)** - Comprehensive theory
- **CS231n (Stanford)** - Computer Vision with CNNs
- **CS224n (Stanford)** - NLP with Deep Learning

### Books:
- **Deep Learning** by Ian Goodfellow (The Bible)
- **Deep Learning with Python** by François Chollet (Keras creator)
- **Hands-On Machine Learning** Part II by Aurélien Géron

### Platforms:
- **Kaggle** - Competitions and datasets
- **Papers with Code** - Latest research with implementations
- **Hugging Face** - Pre-trained models and datasets

---

## ✅ Completion Checklist

- [ ] Understand neural network basics
- [ ] Built simple neural network from scratch
- [ ] Trained CNN for image classification
- [ ] Used LSTM for sequence data
- [ ] Applied transfer learning
- [ ] Implemented data augmentation
- [ ] Tuned hyperparameters
- [ ] Deployed deep learning model
- [ ] Completed 3+ DL projects

---

## 🎯 Time Estimate

**Total**: 4-6 weeks with 12-15 hours/week

---

[⬅️ Back to AI/ML](../)

# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program:
**Developed By:**
- **Name:** SHYAM S  
- **Register Number:** 212223240156

### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread().
```python
bgr_img = cv2.imread('Eagle_in_Flight.jpg')
```

#### 2. Print the image width, height & Channel.
```python
height, width, channels = bgr_img.shape

(width, height, channels)
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(cv2.cvtColor(bgr_img, cv2.COLOR_BGR2RGB))
plt.title("Eagle Image")
plt.axis("off")
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite("Eagle_in_Flight.png", bgr_img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
img_color = cv2.imread("Eagle_in_Flight.png")
img_color = cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(img_color)
plt.title("Colour Image")
plt.axis("off")
plt.show()

height, width, channels = img_color.shape
(width, height, channels)
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
crop = img_color[80:500, 70:620]

plt.imshow(crop)
plt.title("Cropped Eagle")
plt.axis("off")
plt.show()
```

#### 8. Resize the image up by a factor of 2x.
```python
resized_img = cv2.resize(img_color, None, fx=2, fy=2, interpolation=cv2.INTER_LINEAR)

plt.imshow(resized_img)
plt.title("2x Resized Image")
plt.axis("off")
plt.show()
```

#### 9. Flip the cropped/resized image horizontally.
```python
flipped_img = cv2.flip(resized_img, 1)

plt.imshow(flipped_img)
plt.title("Horizontally Flipped Eagle")
plt.axis("off")
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
bgr_img = cv2.imread("Apollo-11-launch.jpg")
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
apollo = cv2.imread("Apollo-11-launch.jpg")

text = "Apollo 11 Saturn V Launch, July 16, 1969"
font_face = cv2.FONT_HERSHEY_PLAIN

cv2.putText(
    apollo,
    text,
    (120, apollo.shape[0] - 30),
    font_face,
    2,
    (255, 255, 255),
    2
)

plt.imshow(cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB))
plt.axis("off")
plt.show()
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
apollo = cv2.imread("Apollo-11-launch.jpg")

cv2.rectangle(
    apollo,
    (450, 50),
    (700, 950),
    (255, 0, 255),
    3
)

plt.imshow(cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB))
plt.axis("off")
plt.show()
```

#### 13. Display the final annotated image.
```python
plt.figure(figsize=(10, 8))
plt.imshow(cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB))
plt.title("Apollo 11 Launch - Annotated")
plt.axis("off")
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```python
boy = cv2.imread("boy.jpg")
```

#### 15. Adjust the brightness of the image.
```python
bright_img = cv2.convertScaleAbs(boy, alpha=1.0, beta=50)

plt.imshow(cv2.cvtColor(bright_img, cv2.COLOR_BGR2RGB))
plt.axis("off")
plt.show()
```

#### 16. Create brighter and darker images.
```python
brighter = cv2.convertScaleAbs(boy, alpha=1.0, beta=50)
darker = cv2.convertScaleAbs(boy, alpha=1.0, beta=-50)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(brighter, cv2.COLOR_BGR2RGB))
plt.title("Brighter")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(darker, cv2.COLOR_BGR2RGB))
plt.title("Darker")
plt.axis("off")

plt.show()
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(boy, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(darker, cv2.COLOR_BGR2RGB))
plt.title("Darker Image")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(brighter, cv2.COLOR_BGR2RGB))
plt.title("Brighter Image")
plt.axis("off")

plt.show()
```

#### 18. Modify the image contrast.
```python
img = boy

matrix1 = np.full(img.shape, 1.1, dtype=np.float32)
matrix2 = np.full(img.shape, 1.2, dtype=np.float32)

img_higher1 = cv2.multiply(img.astype(np.float32), matrix1).astype(np.uint8)
img_higher2 = cv2.multiply(img.astype(np.float32), matrix2).astype(np.uint8)

img_lower = cv2.convertScaleAbs(img, alpha=0.8, beta=0)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB))
plt.title("Lower Contrast")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB))
plt.title("Higher Contrast")
plt.axis("off")

plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(boy)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(b, cmap="gray")
plt.title("Blue Channel")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(g, cmap="gray")
plt.title("Green Channel")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(r, cmap="gray")
plt.title("Red Channel")
plt.axis("off")

plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged = cv2.merge((b, g, r))

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(boy, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(merged, cv2.COLOR_BGR2RGB))
plt.title("Merged Image")
plt.axis("off")

plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv = cv2.cvtColor(boy, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(h, cmap="gray")
plt.title("Hue (H)")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(s, cmap="gray")
plt.title("Saturation (S)")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(v, cmap="gray")
plt.title("Value (V)")
plt.axis("off")

plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge((h, s, v))
merged_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(boy, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB))
plt.title("Merged HSV Image")
plt.axis("off")

plt.show()
```

## Output:
The notebook successfully demonstrates:

- Image reading and display
- Image saving
- Cropping
- Resizing
- Flipping
- Text annotation
- Shape drawing
- Brightness adjustment
- Contrast adjustment
- RGB channel split and merge
- HSV channel split and merge

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.


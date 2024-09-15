# MAVericks | Entity Extraction from Images
<img src="https://github.com/user-attachments/assets/39c46fdc-7f20-43a7-b4ea-144c78821feb" alt="Team Logo"  height="150">

# Problem Statement
<h2>Feature Extraction from Images</h2>
In this hackathon, the goal is to create a machine learning model that extracts entity values from images. This capability is crucial in fields like healthcare, e-
commerce, and content moderation, where precise product information is vital. As digital marketplaces expand, many products lack detailed textual
descriptions, making it essential to obtain key details directly from images. These images provide important information such as weight, volume, voltage,
wattage, dimensions, and many more, which are critical for digital stores.

## Data Description:
The dataset consists of the following columns:
1. index: A unique identifier (ID) for the data sample.
2. image-link: Public URL where the product image is available for download. Example link - https://m.media-amazon.com/images/l/71XfHPR36-L.jpg To
download images, use the download_images function from src/utils. py. See sample code in src/test. ipynb.
3. group_id: Category code of the product.
4. entity_name: Product entity name. For example, "item_weight".
5. entity_value: Product entity value. For example, "34 gram".


## Proposed Solution

### ML Approach

The approach combines several machine learning techniques and models to achieve accurate entity metric extraction:

1. Optical Character Recognition (OCR)
2. Named Entity Recognition (NER)
3. Image-based text extraction
4. Rule-based post-processing

To explain the machine learning models and libraries used in your project, you can present them in a structured and detailed manner. Below is a formatted version that would fit well in your README:

## Machine Learning Models and Libraries Used

### 1. **Florence-2-large**
   - **Description:** Florence-2-large is a multi-modal model designed to understand both text and images. It helps in extracting text-based information from images and provides a deeper contextual understanding of the visual content.
   - **Use Case:** In this project, we utilized Florence-2-large to extract relevant text from images, helping to bridge the gap between visual content and textual data for accurate information retrieval.

### 2. **PaddleOCR**
   - **Description:** PaddleOCR is a deep learning-based Optical Character Recognition (OCR) system. It is particularly effective for recognizing text in challenging layouts and orientations, such as rotated or non-standard text.
   - **Use Case:** This OCR tool was crucial in extracting text from images where the content was skewed, rotated, or otherwise difficult to process using traditional methods. PaddleOCR ensured high accuracy in extracting the necessary textual information from these images.

### 3. **spaCy**
   - **Description:** spaCy is an open-source Python library used for advanced natural language processing (NLP) tasks such as tokenization, part-of-speech tagging, and named entity recognition.
   - **Use Case:** spaCy was used to process and analyze the extracted text from images, enabling the identification of key information such as entities and metrics. Its efficiency in text processing made it ideal for our task of information extraction.

### 4. **Custom NER Model**
   - **Description:** A custom Named Entity Recognition (NER) model built using spaCy. This model is tailored to identify and classify specific entities (like voltage, weight, and height) from the text extracted using PaddleOCR.
   - **Use Case:** The custom NER model played a critical role in identifying relevant entities from the text data. By classifying metrics such as weight, volume, and dimensions, it facilitated accurate extraction of important information for further processing.

### 5. **OpenCV (cv2)**
   - **Description:** OpenCV (Open Source Computer Vision Library) is one of the most widely used libraries for computer vision tasks such as image preprocessing, object detection, and image manipulation.
   - **Use Case:** In this project, OpenCV was used to preprocess images by detecting and cropping regions of interest (ROI), enhancing the overall image clarity for text extraction. Additionally, OpenCV helped in detecting structural elements like lines, improving the accuracy of the text and entity extraction process.

### 6. **Hough Line Transform**
   - **Description:** The Hough Line Transform is a computer vision algorithm used to detect straight lines in an image. It transforms the image into a parameter space and identifies the lines present in the image.
   - **Use Case:** This algorithm was used to detect lines within the images, helping to identify and separate different sections or regions of the image. It enhanced the text extraction process by ensuring the structural integrity of the layout.

---

## Pipeline Overview

### 1. **Image Preprocessing**
   - **Description:** The process begins by loading the image from a provided URL. To enhance the clarity and focus on relevant areas, a Gaussian blur is applied to smooth the image, followed by edge detection using the **Canny algorithm**. 
   - **Hough Line Transform** is then employed to detect key lines and measurement indicators within the image, helping to narrow down the analysis to the essential parts of the image for accurate text and entity extraction.

### 2. **Text Extraction**
   - **Florence-2-large** is used as the primary model for text extraction with an OCR-specific task prompt. It processes the image to extract textual data, particularly focusing on key information relevant to the task.
   - Additionally, **PaddleOCR** is applied as a complementary method, especially useful for extracting text from challenging or distorted parts of the image where the primary model may struggle.

### 3. **Entity Recognition**
   - Once the text has been extracted, the project utilizes a **custom Named Entity Recognition (NER) model** to identify key entities such as measurements, units, and other relevant attributes.
   - The text is processed, and the NER model differentiates between various entities. It helps classify the extracted information, which is crucial for identifying entity-specific details like voltage, weight, or dimensions.

### 4. **Metric Extraction and Normalization**
   - **Regular expressions (Regex)** are employed to extract numerical values and units from the text. The system detects measurements and formats them into a standardized form (e.g., grams, meters).
   - After extracting the metrics, a thorough screening of the gathered data is performed to ensure only essential and accurate information is retained. This step ensures that only the most relevant data is taken from the **Florence-2-large** model's output.

### 5. **Entity-Specific Processing**
   - Specialized functions are implemented to handle each entity type separately. For instance, voltage, wattage, weight, volume, and dimensions are processed with tailored algorithms to extract and calculate the most accurate values for each entity.
   - These entity-specific functions ensure that the metrics are relevant to the context and domain of the entity, enhancing the accuracy of the pipeline’s results.

### 6. **Result Formatting**
   - The final step involves formatting the extracted and processed data into standardized numerical values.
   - Metric units are expanded and clarified, ensuring the results are presented in a consistent and interpretable format (e.g., `12.5 kilogram` or `1.0 meter`).

---

## Output Images

<div style="display: flex; justify-content: space-between; align-items: center; gap: 20px;">
    <img src="https://github.com/user-attachments/assets/c67ffb62-cb0b-4038-8104-1b43668a9e6e" alt="Image 1" style="width: 33%; height: auto;">
    <img src="https://github.com/user-attachments/assets/15e75b8b-579c-45ce-bedb-a08d0e7991d7" alt="Image 2" style="width: 33%; height: auto;">
    <img src="https://github.com/user-attachments/assets/fdeb2313-7fa3-40ea-b82d-6c4861621bb8" alt="Image 3" style="width: 33%; height: auto;">
</div>

## Conclusion
In this project, we tackled the challenge of extracting entity values from images, focusing on metrics such as weight, volume, and dimensions. By combining advanced machine learning techniques, including OCR and NER, and leveraging powerful models like Florence-2-large, PaddleOCR, and custom NER models, we were able to develop an effective pipeline for feature extraction. Through careful image preprocessing with OpenCV, structural detection using the Hough Line Transform, and meticulous text extraction and processing, our solution provides accurate and reliable information from images. This approach is critical for industries such as e-commerce and healthcare, where accurate and detailed product information is essential for decision-making. The result is a robust system capable of processing complex images and delivering precise, entity-specific details for practical use cases.

---

## Authors 

<div align="left"> 
  <table>
  <tr align="left">
   <td>

   ## Meghanand Gejjela
   <p align="center">
   <img src = "https://raw.githubusercontent.com/Megh-Zyke/Histify/main/images/meghs.jpg"  height="120" alt="Meghanand">
   </p>
   <p align="center">
   <a href = "https://github.com/Megh-Zyke"><img src = "http://www.iconninja.com/files/241/825/211/round-collaboration-social-github-code-circle-network-icon.svg" width="36" height = "36"/></a>
   <a href = "https://www.linkedin.com/in/meghanandgejjela/">
   <img src = "http://www.iconninja.com/files/863/607/751/network-linkedin-social-connection-circular-circle-media-icon.svg" width="36" height="36"/>
   </a>
   </p>
    <strong>Computer Vision | Natural Langauge Processing<strong>
    </td>
    <td>


   ## Anirudh R Kavle
   <p align="center">
   <img src = "https://raw.githubusercontent.com/Megh-Zyke/Histify/main/images/Anirudh.jpg"  height="120" alt="Anirudh">
   </p>
   <p align="center">
   <a href = "https://github.com/Anirudh-Kavle"><img src = "http://www.iconninja.com/files/241/825/211/round-collaboration-social-github-code-circle-network-icon.svg" width="36" height = "36"/></a>
   <a href = "https://www.linkedin.com/in/anirudhkavle28/">
   <img src = "http://www.iconninja.com/files/863/607/751/network-linkedin-social-connection-circular-circle-media-icon.svg" width="36" height="36"/>
   </a>
   </p>
    <strong>Natural Language Processing | Vision Language Models <strong>
    </td>
    <td>
      
   ## Vidhyuth Kasturirangan 
   <p align="center">
   
   <img src = "https://media.licdn.com/dms/image/v2/D5603AQGVXkt5kDr3Xg/profile-displayphoto-shrink_800_800/profile-displayphoto-shrink_800_800/0/1690130175022?e=1732147200&v=beta&t=WJQxkGm134wScHHkr4f0ZNkFMRMCCnCKeM_F7d8e7qs"  height="120" alt="Vidhyuth">
   </p>
   <p align="center">
   <a href = "https://github.com/Vid2714"><img src = "http://www.iconninja.com/files/241/825/211/round-collaboration-social-github-code-circle-network-icon.svg" width="36" height = "36"/></a>
    
   <a href = " https://www.linkedin.com/in/vidhyuthk316/">
   <img src = "http://www.iconninja.com/files/863/607/751/network-linkedin-social-connection-circular-circle-media-icon.svg" width="36" height="36"/>
   </a>
   </p>
    <strong>Data Analysis | Natural Language Processing  </strong>
    </td>
    </table>

  






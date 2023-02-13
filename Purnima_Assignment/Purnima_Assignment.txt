import cv2
import pytesseract
from PIL import Image
import numpy as np

pytesseract.pytesseract.tesseract_cmd = 'C:\\Program Files\\Tesseract-OCR\\tesseract.exe'

class fetch_text_from_image:
    def read_img(self, list_of_images):
        for file_path in list_of_images:
            img = cv2.imread(file_path)
            no_removal = self.noise_removal(img)
            cv2.imwrite("updateimagess3.png", no_removal)
            self.get_text("updateimagess3.png")
        

    def noise_removal(self, file_path):
        kernel = np.ones((1,1), np.uint8)
        image1 = cv2.dilate(file_path, kernel, iterations=1)
        image2 = cv2.morphologyEx(image1, cv2.MORPH_CLOSE, kernel)
        image3 = cv2.medianBlur(image2, 3)
        return image3


    def get_text(self, file_path):
        raw_img = Image.open(file_path)
        text = pytesseract.image_to_string(raw_img)
        # Below print is only for separation of all documents
        print("---------------------------------------------------------------------------")
        print(text)


if __name__ == "__main__":
    obj = fetch_text_from_image()
    list_of_images = [r"C:\Users\Purnima\Desktop\Purnima_Assesment\Resolute AI Software\Task1\1.jpg", r"C:\Users\Purnima\Desktop\Purnima_Assesment\Resolute AI Software\Task1\2.jpg", r"C:\Users\Purnima\Desktop\Purnima_Assesment\Resolute AI Software\Task1\3.jpg"]

    read_images = obj.read_img(list_of_images)
    print("Program Executes Successfully!!!")





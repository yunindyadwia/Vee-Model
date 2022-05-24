import cv2
import dlib
import time
import threading
import math
import datetime
import os
import openpyxl
from openpyxl import load_workbook
import matplotlib.pyplot as plt
import numpy as np
from skimage import util
from skimage.io import imread
from skimage.filters import threshold_otsu
from skimage import measure
from skimage.measure import regionprops
import matplotlib.patches as patches
import sklearn
import joblib

SNo = int(1)
counter = 0
sheet = {}
now = datetime.datetime.now()

mainFilename = 'C:\\Users\yunin\OneDrive\Dokumen\data_measurements.xlsx'

if not(os.path.isfile(mainFilename)):
    mwb = openpyxl.Workbook() #main work book
    #main_sheet = mwb.create_sheet('main_sheet')
    #main_sheet = mwb.worksheets
    main_sheet=mwb.active  
    #main_sheet = main_sheet.title
    main_sheet.cell(row=1, column=1).value = 'VehicleID'
    main_sheet.cell(row=1, column=2).value = 'Vehicle_Number'

sheet[0] = mwb.create_sheet('sheet%d' %counter)
    # ws[counter] = mwb.worksheets[counter]
    sheet[0] = mwb.active
    a = 'Daily Vehicles'
    day = now.day
    b = str(str(a) + str(day) + '.' + str(now.month) + '.' + str(now.year))
    sheet[0].title = b
    sheet[0].cell(row=1, column=1).value = 'VehicleID'
    sheet[0].cell(row=1, column=2).value = 'Date'
    sheet[0].cell(row=1, column=3).value = 'Time'
    sheet[0].cell(row=1, column=4).value = 'Camera'
    sheet[0].cell(row=1, column=5).value = 'Speed'
    sheet[0].cell(row=1, column=6).value = 'Number Plate'
    
 def detection(image_1):
    #print(img)
    height = 900
    width = 700
    img = cv2.cvtColor(image_1, cv2.COLOR_RGB2GRAY)
    speedometer_image.jpeg = cv2.resize(img, (width,height))
    img_1 = cv2.resize(img, (width,height))
    # speedometer_image = imread("speedometer_image.jpeg", = True)
    # it should be a 2 dimensional array

    # the next line is not compulsory however, a speedometer scale pixel
    # in skimage ranges between 0 & 1. multiplying it with 255
    # will make it range between 0 & 255 (something we can relate better with
    
    
    speedometer_image = speedometer_image * 255
    #fig, (ax1, ax2) = plt.subplots(1, 2)
    #ax1.imshow(speedometer_image, cmap="speedometer")
    threshold_value = threshold_otsu(speedometer_image)
    binary_car_image = speedometer_image > threshold_value
    #print(binary_car_image)
    #ax2.imshow(binary_speedometer_image, cmap="speedometer")
    # ax2.imshow(speedometer_image, cmap="speedometer")
    #plt.show()

    # CCA (finding connected regions) of binary image


    # this gets all the connected regions and groups them together
    label_image = measure.label(binary_speedometer_image)

    #print(label_image.shape[0]) #height of the image
    #print(label_image.shape[1]) #width of the image
    # getting the maximum width, height and minimum width and height that a license plate can be

    #plate_dimensions0 = (0.01*label_image.shape[0], 0.03*label_image.shape[0], 0.10*label_image.shape[1], 0.15*label_image.shape[1])
    plate_dimensions = (0.06*label_image.shape[0], 0.13*label_image.shape[0], 0.085*label_image.shape[1], 0.2*label_image.shape[1])
    plate_dimensions2 = (0.06*label_image.shape[0], 0.18*label_image.shape[0], 0.15*label_image.shape[1], 0.25*label_image.shape[1])
    min_height, max_height, min_width, max_width = plate_dimensions
    speedometer_objects_cordinates = []
    speedometer_like_objects = []

    #print(min_height, ' ', max_height, ' ', min_width, ' ', max_width)

    #fig, (ax1) = plt.subplots(1)
    #ax1.imshow(gray_car_image, cmap="gray")
    flag =0
    go = 0
    # regionprops creates a list of properties of all the labelled regions

    
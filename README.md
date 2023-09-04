# Bullet
Bullet Target

import cv2
import numpy as np
import pandas as pd


import tkinter
import cv2
import numpy as np
import pandas as pd
from tkinter import *
from PIL import Image
from PIL import ImageTk
from tkinter import messagebox
from tkinter import ttk 
import imutils
import sqlite3
from tkinter.ttk import Combobox
import openpyxl, xlrd
from openpyxl import Workbook
import pathlib
from datetime import date

cap = cv2.VideoCapture(0)

frame_width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
frame_height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
fps = int(cap.get(cv2.CAP_PROP_FPS))
print("width",frame_width)
print("height",frame_height)

df = np.zeros((100000, 4))

i=0

n_tiro = 0

imagen = cv2.imread('numero_1.jpg') 
res_1 = cv2.resize(imagen, dsize=(650, 650))

while n_tiro < 111111:
    ret, frame = cap.read()
    if ret is False:
        break
    
    frame = cv2.resize(frame, dsize=(650, 650))

    rows, cols, _ = frame.shape
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    gauss = cv2.GaussianBlur(gray, (7, 7),0)
    ret, threshold = cv2.threshold(gauss, 250, 255, cv2.THRESH_BINARY_INV)
    contours, hierarchy  =  cv2.findContours(threshold, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
    contours =sorted(contours, key=lambda x: cv2.contourArea(x))
    
    a1 = 33 
    a2 = 60
    a3 = 79
    a4 = 98
    a5 = 122
    a6 = 147
    a7 = 171
    a8 = 195
    a9 = 220
    a10 = 244
    
    b1 = 44
    b2 = 80
    b3 = 105
    b4 = 130
    b5 = 163
    b6 = 195
    b7 = 228
    b8 = 260
    b9 = 293
    b10 = 325
    
    
    for cnt in contours:
        x, y, w, h = cv2.boundingRect(cnt)
        puntaje = 0
        cv2.drawContours(frame, [cnt], -1,(0,0,255),3)
        cv2.rectangle(frame, (x, y), (x + w, y + h), (255,0,0), 3)
        #cv2.line(frame, (x + int(w/2), 0), (x + int(w/2), rows), (0, 255,0), 5)
        #cv2.line(frame, (0, y + int(h/2)), (cols, y + int(h/2)), (0, 255,0), 1)
        #cv2.circle(frame,(x + int(w/2), y + int(h/2)),2,(255,0,0),-1)
        
        #print("h",h)
        #print("w",w)
        #print(x)
        #print("col",cols)
        #print("row",rows)
        
        x = x + int(w/2)
        
        y = y + int(h/2)
        
        y_t = 325 - y
        
        x_t = int((325 - x)*1.33)
        
        x = x + 2*x_t
        
        cir1 = cv2.circle(frame,(x , y),10,(0,255,0),-1)
        
        if w != 650 and h != 650:
        
            cir = cv2.circle(res_1,(x ,y ),10,(0,255,0),-1)
        
        if (w == 650 and h == 650):
                
            #n_tiro  = None
            x       = None
            y       = None
            puntaje = 0
                
            df[i] = n_tiro, x, y, puntaje
                
            break
            
        else:
            #x = x + int(w/2) 
            #- int(cols/2) 
            #y = -y - int(h/2) 
            #+ int(rows/2)
            #print(x,y) 
            n_tiro = n_tiro + 1
                
            if (0 <= pow(b10*x_t, 2) + pow(a10*y_t, 2) <= pow(a10*b10, 2)):
                puntaje = 10
                
                
            elif ((pow(b10*a10, 2) < pow(b10*x_t, 2) + pow(a10*y_t, 2)) and (pow(b9*x_t, 2) + pow(a9*y_t, 2) <= pow(a9*b9, 2))):
                puntaje = 9
                
                    
            elif ((pow(b9*a9, 2) < pow(b9*x_t, 2) + pow(a9*y_t, 2)) and (pow(b8*x_t, 2) + pow(a8*y_t, 2) <= pow(a8*b8, 2))):
                puntaje = 8
                
            
            elif ((pow(b8*a8, 2) < pow(b8*x_t, 2) + pow(a8*y_t, 2)) and (pow(b7*x_t, 2) + pow(a7*y_t, 2) <= pow(a7*b7, 2))):
                puntaje = 7
                
            elif ((pow(b7*a7, 2) < pow(b7*x_t, 2) + pow(a7*y_t, 2)) and (pow(b6*x_t, 2) + pow(a6*y_t, 2) <= pow(a6*b6, 2))):
                puntaje = 6
                
            elif ((pow(b6*a6, 2) < pow(b6*x_t, 2) + pow(a6*y_t, 2)) and (pow(b5*x_t, 2) + pow(a5*y_t, 2) <= pow(a5*b5, 2))):
                puntaje = 5
    
            elif ((pow(b5*a5, 2) < pow(b5*x_t, 2) + pow(a5*y_t, 2)) and (pow(b4*x_t, 2) + pow(a4*y_t, 2) <= pow(a4*b4, 2))):
                puntaje = 4
    
            elif ((pow(b4*a4, 2) < pow(b4*x_t, 2) + pow(a4*y_t, 2)) and (pow(b3*x_t, 2) + pow(a3*y_t, 2) <= pow(a3*b3, 2))):
                puntaje = 3
                
            elif ((pow(b3*a3, 2) < pow(b3*x_t, 2) + pow(a3*y_t, 2)) and (pow(b2*x_t, 2) + pow(a2*y_t, 2) <= pow(a2*b2, 2))):
                puntaje = 2
                    
            elif ((pow(b2*a2, 2) < pow(b2*x_t, 2) + pow(a2*y_t, 2)) and (pow(b1*x_t, 2) + pow(a1*y_t, 2) <= pow(a1*b1, 2))):
                puntaje = 1
                
                    
            elif (pow(b1*a1, 2) < pow(b1*x_t, 2) + pow(a1*y_t, 2)):
                     
                puntaje = 0
        
            #print(puntaje)
            #df[i] = x, y, puntaje
            print("position (x,y,puntaje):", x_t, y_t, puntaje)
            #print("position (n_tiro,x,y,puntaje):", n_tiro, x, y, puntaje)
        
        break
        
    i = i + 1

    
    cv2.namedWindow('frame', cv2.WINDOW_NORMAL)
    cv2.resizeWindow('frame',width = 650, height = 650)
    cv2.imshow("frame" , cir1)
    
    if w != 650 and h != 650:
        cv2.namedWindow('cicte', cv2.WINDOW_NORMAL)
        cv2.resizeWindow('cicte',width = 840, height = 1200)
        cv2.imshow('cicte_1',cir)
    elif w == 650 and h == 650:
        cv2.namedWindow('cicte', cv2.WINDOW_NORMAL)
        cv2.resizeWindow('cicte',width = 840, height = 1200)
        cv2.imshow('cicte_1',res_1)
    
    
    
    #output1.write(threshold)
    #output2.write(gauss)
    #output3.write(frame)
    key = cv2.waitKey(30)

    if key == 27:
        break

#df = pd.DataFrame(df, columns = ['x','y','Puntaje'])

#print(df)
    
cv2.destroyAllWindows()

#file_name = 'Libro1.csv'
  
# saving the excelsheet
#df.to_csv(file_name)

# DolarLatino
DolarLAtino
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sun Apr 21 19:33:47 2019

@author: leonardomelendez
"""
import matplotlib.pyplot as plt
import requests
import urllib.request
import time
from bs4 import BeautifulSoup
from scipy import stats 
import numpy as np
import random
import sys

#paises a comparar
def comparar(paisUno,pasiDos):
    #cambio=productoDePaisUno/productoDePaisDo
    return 

def pagina(pais,rubro):
        
    return





#response = requests.get(url)
 
#f = open("PayPal _ Activité.html", "r")
#response = f.readlines()
#f.close()

#soup = BeautifulSoup(response.text, "html.parser")



def listadepaises():
    #
    url = 'https://listado.mercadolibre.com'
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    linkPaises=[]
    for a in soup.find_all('a'): 
        linkPaises.append(a['href'])
    return linkPaises


paises=['https://www.mercadolibre.com.ar',
'https://www.mercadolibre.com.bo',
 'https://www.mercadolibre.cl',
 'https://www.mercadolibre.com.co']#,
 #'https://www.mercadolibre.co.cr',
 #'https://www.mercadolibre.com.do',
 #'https://www.mercadolibre.com.ec',
 #'https://www.mercadolibre.com.gt',
 #'https://www.mercadolibre.com.hn',
 #'https://www.mercadolibre.com.ni',
 #'https://www.mercadolibre.com.pa',
 #'https://www.mercadolibre.com.py',
 #'https://www.mercadolibre.com.pe',
 #'https://www.mercadolibre.com.sv',
 #'https://www.mercadolibre.com.uy',
 #'https://www.mercadolibre.com.ve']
#'https://www.mercadolivre.com.br',
#'https://www.mercadolibre.com.mx',
rubros=['serpiente-cuna']#zapatos


#Matriz pais rubro 
GranMatriz=np.zeros((len(rubros), len(paises)))



def Preciodelrubro(hompais,rubro):
    VerifSiguiente='siguiente'
    numeroPagina=0
    valores=[]
    while len(VerifSiguiente) > 1:
    
        #pais='ve'
        #rubro='zapatos'
        #rubro='serpiente-cuna'
        ArticulosXPag=50
    
        numerodeArticulo=1+ArticulosXPag*numeroPagina
    
        #construccion de la pagina 
        url = homepais+'/'+rubro+'_Desde_'+ str(numerodeArticulo) +'_Tienda_all'#_PublishedToday_YES
        
        #url = 'https://listado.mercadolibre.com.'+pais+'/'+rubro+'_Desde_'+ str(numerodeArticulo) +'_Tienda_all'#_PublishedToday_YES
        #url='https://listado.mercadolibre.com.ve/ropa/zapatos_Desde_2051'
        print(url)
        response = requests.get(url)
        soup = BeautifulSoup(response.text, "html.parser")
    
        # verificar que hay un siguiente 
        VerifSiguiente=soup.findAll('a',{'class':'andes-pagination__link prefetch'})
        #[0].getText()
    
        #print('verifsiguientees',VerifSiguiente)
        #print('el largo es:',len(VerifSiguiente))
    
    
        #extraer todos los precios 
        Precios=soup.findAll('span',{'class':'price__fraction'})
        #print(Precios)
        #print('esta es la entrad')
    

        for i,element in enumerate(Precios): 
            #print(valores)
            valores.append(int(element.getText().replace(".", "")))
            
            
            #one_a_tag.append(soup.findAll(class_='netAmount vx_h4 ')
            #link = one_a_tag['span']
            #element['span']
            #h=element.finAll(class_="value")
            #ele=BeautifulSoup(element.text, "html.parser")
            #k=ele.finAll(class_="value")
            #print (h)
        
            #k=soup.findAll({'span','div'},{'class':{'value','listing-title'}})
        numeroPagina=numeroPagina+1
        print(numeroPagina)
        
        
  

#one_a_tag=[]
#for i in range(0,len(soup.findAll(class_='netAmount vx_h4 '))): #'a' tags are for links
    #one_a_tag.append(int(soup.findAll(class_='netAmount vx_h4 ')[i].get_text().replace(".", "")))
    #link = one_a_tag['span']
    #time.sleep(0.1) #pause the code for a sec
    


#print (promediarLista(one_a_tag))
#Ordenamos los valores 
#valores.sort()
#valores.sort(reverse=True)
    print('los valores son :',valores)
    print('el largo de los valores es:',len(valores))
    if len(valores)>0:
        
        moda= stats.mode(valores)[0][0]
        mediana=np.median(valores)
        media=np.mean(valores)
        print('La moda es:',moda,'La mediana es:',mediana,'La media es:',media)
    
        plt.figure(figsize=(5,5))
        plt.plot(valores,'D')
        plt.axhline(y=stats.mode(valores)[0][0], color='r', linestyle='-')
        plt.axhline(y=np.median(valores), color='g', linestyle='-')
        plt.axhline(y=np.mean(valores), color='b', linestyle='-')
        plt.ylabel('Precio')
        plt.show()
        plt.figure(figsize=(5,5))
        plt.hist(valores)
        plt.ylabel('Precio')
        plt.show()
        tiempoEspera=random.uniform(1, 4)
        print(tiempoEspera)
        time.sleep(tiempoEspera)
        print('La moda es:',moda,'La mediana es:',mediana,'La media es:',media)
   
    else:
        moda=0
    return moda

for homepais in paises:
    print('este es el homepais',homepais)
    lin=paises.index(homepais)
    homepais=homepais.replace("www.", "listado.")
    for rubro in rubros:
        
        col=rubros.index(rubro)
        
        
        GranMatriz[col,lin]= Preciodelrubro(homepais,rubro)
        #primero busco en argentina zapatos camisas y pantalones 
        #dame la media de los zapatos 
        #crear una matriz cruzada de valores 
        print("esta es la gran matriz",GranMatriz)
        time.sleep(4)
        

monedas=GranMatriz[0]

def promedio():
    #Esta funcion devuelve la media la mediana o la moda de una matriz 
    GranMatriz=np.random.randint(5, size=(2, 4))
    print(GranMatriz)
    vector=[]
    print (vector)
    GranMatriz[:,0].size
    
    for i in range(GranMatriz[0,:].size):
        vectordePrecios=GranMatriz[:,i]
        moda= stats.mode(vectordePrecios)[0][0]
        mediana=np.median(vectordePrecios)
        media=np.mean(vectordePrecios)
        vector.append(media)
        print("estaeslamedia",vector)
    return vector

promedio()




nombres=[]
for element in paises:
    element.replace("https://www.mercadolibre.","")
    element.replace("com.","")
    element.replace("co.","")
    nombres.append(element)
    
    
    
def comparare(moneda,nombres):
    vectorcambio=[]
    for elemento in moneda:
        for elementi in moneda:
            if elemento==0:
                elemento=1
                
            pais1=nombres[moneda.index(elementi)]
            pais2=nombres[moneda.index(elemento)]
                #elementi=1
            #print(elementi,elemento)
            cambio=elementi/elemento
            vectorcambio.append(cambio)
            print("El cambio entre el ",pais1,"y el ",pais2,"es de",cambio)
    return vectorcambio

comparare(monedas,nombres)

sys.exit()
time.sleep(20)

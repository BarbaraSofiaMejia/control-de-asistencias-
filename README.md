import tkinter as tk
from tkinter import messagebox
import cssv
import os 
ARCHIVO="Empleados.csv"


if not os.path.exists(ARCHIVO).
witch open(ARCHIVO,"w",newline="") as f :
 writer =  csv.writer(f)
 writer.writerow(["Nombre" , "Apellido" , "Puesto" , "Departamento"])

 
 def empleado_existe(nombre, apellido):
    with open(ARCHIVO, "r") as f:
        reader = csv.DictReader(f)
        for fila in reader:
            if fila["Nombre"].strip().lower() == nombre.strip().lower() and fila["Apellido"].strip().lower() == apellido.strip().lower():
                return True
    return False

  
    
    
    

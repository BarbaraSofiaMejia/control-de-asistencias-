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

def registrar_empleado():
    ventana = tk.Toplevel()
    ventana.title("Registrar Empleado")
    ventana.geometry("300x250")

 tk.Label(ventana, text="Nombre:").pack()
    nombre = tk.Entry(ventana)
    nombre.pack() 
    
   tk.Label(ventana, text="Apellido:").pack()
    apellido = tk.Entry(ventana)
    apellido.pack()

   tk.Label(ventana, text="Puesto:").pack()
    puesto = tk.Entry(ventana)
    puesto.pack()
    
   tk.Label(ventana, text="Departamento:").pack()
    departamento = tk.Entry(ventana)
    departamento.pack()

   def guardar():
        if nombre.get() and apellido.get() and puesto.get() and departamento.get():
            with open(ARCHIVO, "a", newline="") as f:
                writer = csv.writer(f)
                writer.writerow([nombre.get(), apellido.get(), puesto.get(), departamento.get()])
            messagebox.showinfo("Éxito", "Empleado registrado.")
            ventana.destroy()
        else:
            messagebox.showwarning("Error", "Todos los campos son obligatorios.")

   tk.Button(ventana, text="Guardar", command=guardar).pack(pady=10)

   
def ver_empleados():
    ventana = tk.Toplevel()
    ventana.title("Lista de Empleados")
    ventana.geometry("400x300")

   texto = tk.Text(ventana)
    texto.pack(fill=tk.BOTH, expand=True)

   with open(ARCHIVO, "r") as f:
        for linea in f:
            texto.insert(tk.END, linea)

    
def eliminar_empleado():
    ventana = tk.Toplevel()
    ventana.title("Eliminar Empleado")
    ventana.geometry("300x150")

   tk.Label(ventana, text="Nombre:").pack()
    nombre = tk.Entry(ventana)
    nombre.pack()

   tk.Label(ventana, text="Apellido:").pack()
    apellido = tk.Entry(ventana)
    apellido.pack()   

   def eliminar():
        if not nombre.get() or not apellido.get():
            messagebox.showwarning("Error", "Completa ambos campos.")
            return

   if not empleado_existe(nombre.get(), apellido.get()):
            messagebox.showerror("Error", "Dato no existente.")
            return

   empleados_actualizados = []
        with open(ARCHIVO, "r") as f:
            reader = csv.DictReader(f)
            for fila in reader:
                if not (fila["Nombre"].strip().lower() == nombre.get().strip().lower() and 
                        fila["Apellido"].strip().lower() == apellido.get().strip().lower()):
                    empleados_actualizados.append(fila)

    
   with open(ARCHIVO, "w", newline="") as f:
            writer = csv.DictWriter(f, fieldnames=["Nombre", "Apellido", "Puesto", "Departamento"])
            writer.writeheader()
            writer.writerows(empleados_actualizados)

   messagebox.showinfo("Éxito", "Empleado eliminado.")
        ventana.destroy()

   tk.Button(ventana, text="Eliminar", command=eliminar).pack(pady=10)




    
  
    
    
    

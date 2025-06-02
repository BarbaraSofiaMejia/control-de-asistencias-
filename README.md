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

   ef registrar_asistencia():
    ventana = tk.Toplevel()
    ventana.title("Registrar Asistencia")
    ventana.geometry("300x150")

   tk.Label(ventana, text="Nombre:").pack()
    nombre = tk.Entry(ventana)
    nombre.pack()

   tk.Label(ventana, text="Apellido:").pack()
    apellido = tk.Entry(ventana)
    apellido.pack()

   def registrar():
        if empleado_existe(nombre.get(), apellido.get()):
            messagebox.showinfo("Éxito", "Asistencia registrada.")
        else:
            messagebox.showerror("Error", "Dato no existente.")
        ventana.destroy()

   tk.Button(ventana, text="Registrar", command=registrar).pack(pady=10)


   tk.Button(ventana, text="Guardar", command=guardar).pack(pady=10)

def registrar_incapacidad():
    ventana = tk.Toplevel()
    ventana.title("Registrar Incapacidad")
    ventana.geometry("300x200")

   tk.Label(ventana, text="Nombre:").pack()
    nombre = tk.Entry(ventana)
    nombre.pack()

   tk.Label(ventana, text="Apellido:").pack()
    apellido = tk.Entry(ventana)
    apellido.pack()

   tk.Label(ventana, text="Días de incapacidad:").pack()
    dias = tk.Entry(ventana)
    dias.pack()

 def guardar():
        if empleado_existe(nombre.get(), apellido.get()):
            messagebox.showinfo("Éxito", f"Incapacidad registrada por {dias.get()} días.")
        else:
            messagebox.showerror("Error", "Dato no existente.")
        ventana.destroy()

   tk.Button(ventana, text="Guardar", command=guardar).pack(pady=10)

def registrar_vacaciones():
    ventana = tk.Toplevel()
    ventana.title("Registrar Vacaciones")
    ventana.geometry("300x200")

   tk.Label(ventana, text="Nombre:").pack()
    nombre = tk.Entry(ventana)
    nombre.pack()

   tk.Label(ventana, text="Apellido:").pack()
    apellido = tk.Entry(ventandef retardos_permisos():
    ventana = tk.Toplevel()
    ventana.title("Retardos y Permisos")
    ventana.geometry("300x200")

   tk.Label(ventana, text="Nombre:").pack()
    nombre = tk.Entry(ventana)
    nombre.pack()

   tk.Label(ventana, text="Apellido:").pack()
    apellido = tk.Entry(ventana)
    apellido.pack()

   tk.Label(ventana, text="Tipo (Retardo/Permiso):").pack()
    tipo = tk.Entry(ventana)
    tipo.pack()

   def guardar():
        if empleado_existe(nombre.get(), apellido.get()):
            messagebox.showinfo("Éxito", f"{tipo.get()} registrado.")
        else:
            messagebox.showerror("Error", "Dato no existente.")
        ventana.destroy()a)
    apellido.pack()

   tk.Label(ventana, text="Fecha de inicio:").pack()
    inicio = tk.Entry(ventana)
    inicio.pack()

   tk.Label(ventana, text="Fecha de fin:").pack()
    fin = tk.Entry(ventana)
    fin.pack()

   def guardar():
        if empleado_existe(nombre.get(), apellido.get()):
            messagebox.showinfo("Éxito", f"Vacaciones registradas del {inicio.get()} al {fin.get()}.")
        else:
            messagebox.showerror("Error", "Dato no existente.")
        ventana.destroy()

   tk.Button(ventana, text="Guardar", command=guardar).pack(pady=10)




    
  
    
    
    

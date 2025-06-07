import tkinter as tk

from tkinter import messagebox, ttk
import csv
import os

from datetime import datetime

ARCHIVO="Empleados.csv"


if not os.path.exists(ARCHIVO):

   with open(ARCHIVO, "w", newline="") as f:
    writer = csv.writer(f)
        writer.writerow([
            "Nombre", "Apellido", "Puesto", "Departamento", "Turno",
           "Fecha Nacimiento", "Sexo", "Último Grado Estudio",
            "Cédula", "Domicilio", "Teléfono", "Correo Electrónico", "Fecha Ingreso"
            
  ])

 def empleado_existe(nombre, apellido):
    with open(ARCHIVO, "r") as f:
        reader = csv.DictReader(f)
        for fila in reader:
            if fila["Nombre"].strip().lower() == nombre.strip().lower() and fila["Apellido"].strip().lower() == apellido.strip().lower():
                return True
    return False

   def crear_entrada(frame, texto, fila):
   ttk.Label(frame, text=texto, background="#FFFFFF").grid(row=fila, column=0, pady=5, sticky="e")
   entrada = ttk.Entry(frame, width=30)
    entrada.grid(row=fila, column=1, pady=5)
    return entrada

def crear_combobox(frame, texto, fila, valores):

   ttk.Label(frame, text=texto, background="#FFFEFE").grid(row=fila, column=0, pady=5, sticky="e")
    combobox = ttk.Combobox(frame, values=valores, state="readonly", width=28)
    combobox.grid(row=fila, column=1, pady=5)
    combobo.current(0)
    return combobox

def registrar_empleado():
    ventana = tk.Toplevel()
    ventana.title("Registrar Empleado")
     ventana.geometry("450x600")
   ventana.configure(bg="#e0f7fa")
    frame = ttk.Frame(ventana, padding="20")
    frame.pack(fill=tk.BOTH, expand=True)

 entradas = {}
   entradas["Nombre"] = crear_entrada(frame, "Nombre:", 0)
   entradas["Apellido"] = crear_entrada(frame, "Apellido:", 1)

   puestos = ["Médico", "Enfermero", "Médico General", "Pediatra", "Otorrinolaringólogo", "Cirujano Plástico"]
    ttk.Label(frame, text="Puesto:", background="#FFFFFF").grid(row=2, column=0, pady=5, sticky="e")
    puesto_cb = ttk.Combobox(frame, values=puestos, state="readonly", width=28)
    puesto_cb.grid(row=2, column=1, pady=5)
    puesto_cb.current(0)
    
   departamento = crear_combobox(frame, "Departamento:", 3, ["1", "2", "3"])
    turno = crear_combobox(frame, "Turno:", 4, ["Matutino", "Vespertino", "Noche"])
    entradas["Fecha Nacimiento"] = crear_entrada(frame, "Fecha de Nacimiento (DD/MM/AAAA):", 5)
    sexo = crear_combobox(frame, "Sexo:", 6, ["Mujer", "Hombre", "Otro"])
    entradas["Último Grado Estudio"] = crear_entrada(frame, "Último Grado de Estudio:", 7)
    entradas["Cédula"] = crear_entrada(frame, "Cédula:", 8)
    entradas["Domicilio"] = crear_entrada(frame, "Domicilio:", 9)
    entradas["Teléfono"] = crear_entrada(frame, "Teléfono:", 10)
    entradas["Correo Electrónico"] = crear_entrada(frame, "Correo Electrónico:", 11)
    entradas["Fecha Ingreso"] = crear_entrada(frame, "Fecha de Ingreso (DD/MM/AAAA):", 12)
    def guardar():
        campos_obligatorios = ["Nombre", "Apellido", "Fecha Nacimiento", "Último Grado Estudio", "Cédula", "Domicilio", "Teléfono", "Correo Electrónico", "Fecha Ingreso"]

   if any(not entradas[c].get().strip() for c in campos_obligatorios) or not puesto_cb.get() or not departamento.get() or not turno.get() or not sexo.get():

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

   ventana = tk.Tk()
ventana.title("Control de Personal")
ventana.geometry("500x350")

tk.Label(ventana, text="Bienvenido al Sistema de Control de Personal", font=("Arial", 14)).pack(pady=50)


def activar_menu():
    ventana.config(menu=menu_principal)
    boton_menu.pack_forget()
    tk.Label(ventana, text="Opciones activadas arriba.", fg="green").pack()

boton_menu = tk.Button(ventana, text="Ir al menú de opciones", font=("Arial", 12), command=activar_menu)
boton_menu.pack(pady=10)

menu_principal = tk.Menu(ventana)
opciones = tk.Menu(menu_principal, tearoff=0)
opciones.add_command(label="Registrar Empleado", command=registrar_empleado)
opciones.add_command(label="Eliminar Empleado", command=eliminar_empleado)
opciones.add_command(label="Registro de Asistencia", command=registrar_asistencia)
opciones.add_command(label="Retardos y Permisos", command=retardos_permisos)
opciones.add_command(label="Incapacidad", command=registrar_incapacidad)
opciones.add_command(label="Vacaciones", command=registrar_vacaciones)

menu_principal.add_cascade(label="Opciones", menu=opciones)

ventana.mainloop()



    
  
    
    
    

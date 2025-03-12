# nuevo-trabajo
import os

class GestorTareas:
    ARCHIVO_TAREAS = "tareas.txt"

    @staticmethod
    def agregar_tarea():
        tarea = input("Ingrese la tarea: ")
        with open(GestorTareas.ARCHIVO_TAREAS, "a", encoding="utf-8") as archivo:
            archivo.write(tarea + "\n")
        print("Tarea agregada.")

    @staticmethod
    def mostrar_tareas():
        if not os.path.exists(GestorTareas.ARCHIVO_TAREAS):
            print("No hay tareas.")
            return
        with open(GestorTareas.ARCHIVO_TAREAS, "r", encoding="utf-8") as archivo:
            tareas = archivo.readlines()
        if tareas:
            print("Tareas:")
            for i, tarea in enumerate(tareas, 1):
                print(f"{i}. {tarea.strip()}")
        else:
            print("No hay tareas.")

    @staticmethod
    def completar_tarea():
        GestorTareas.mostrar_tareas()
        if not os.path.exists(GestorTareas.ARCHIVO_TAREAS):
            return
        try:
            numero = int(input("Número de tarea completada: ")) - 1
            with open(GestorTareas.ARCHIVO_TAREAS, "r", encoding="utf-8") as archivo:
                tareas = archivo.readlines()
            if 0 <= numero < len(tareas):
                del tareas[numero]
                with open(GestorTareas.ARCHIVO_TAREAS, "w", encoding="utf-8") as archivo:
                    archivo.writelines(tareas)
                print("Tarea completada.")
            else:
                print("Número inválido.")
        except ValueError:
            print("Ingrese un número válido.")

if __name__ == "__main__":
    while True:
        opcion = input("\n1. Agregar tarea\n2. Mostrar tareas\n3. Completar tarea\n4. Salir\nSeleccione una opción: ")
        if opcion == "1":
            GestorTareas.agregar_tarea()
        elif opcion == "2":
            GestorTareas.mostrar_tareas()
        elif opcion == "3":
            GestorTareas.completar_tarea()
        elif opcion == "4":
            break
        else:
            print("Opción inválida.")
# Ejemplo de uso
nombre_archivo = "tareas.txt"

while True:
    print("\nMenú:")
    print("1. Agregar tarea")
    print("2. Mostrar tareas")
    print("3. Marcar tarea como completada")
    print("4. Salir")
    
    opcion = input("Seleccione una opción: ")
    
    if opcion == '1':
        agregar_tarea(nombre_archivo)
    elif opcion == '2':
        mostrar_tareas(nombre_archivo)
    elif opcion == '3':
        marcar_tarea_completada(nombre_archivo)
    elif opcion == '4':
        break
    else:
        print("Opción inválida. Intente de nuevo.")
        

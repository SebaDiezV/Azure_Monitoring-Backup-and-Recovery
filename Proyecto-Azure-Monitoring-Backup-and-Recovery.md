# Proyecto 3 : Monitoring, Backup, and Recovery

## Temas Tratados
Azure Monitor, Alerts, Backup, Encryption, Protocols, Log Queries

## Resumen
Este proyecto se centra en configurar Azure Monitor para la supervisión del rendimiento, habilitar copias de seguridad para la recuperación de datos, configurar la recuperación ante desastres con Site Recovery y analizar registros con Log Analytics.

## Escenario
Una empresa desea supervisar su infraestructura para detectar problemas de rendimiento, garantizar la recuperación de datos en caso de falla, aplicar transferencias de datos seguras y analizar registros para obtener información.

>**Nota**: Debes crear una máquina virtual para este proyecto, Se crea una VM de tamaño Standard_DC2s_v2 con una imagen Windows Server 2022 Datacenter: Azure Edition


## Tarea 1: Configura Azure Monitor para la VM
1. Dirigete a la VM, ingresa a  **Supervisión** > **Información** y selecciona **Azure Monitor**
<img width="472" alt="01" src="https://github.com/user-attachments/assets/03063cc5-f5cb-4ee5-8338-cd9a910eba14" />

2. Ingresa a **configuración de Insights**
<img width="624" alt="02" src="https://github.com/user-attachments/assets/153552a0-7699-47d9-89ae-df8316bc08f9" />

3. En el icono de la VM, selecciona Habilitar y en la siguiente pantalla > Habilitar
<img width="545" alt="03" src="https://github.com/user-attachments/assets/bac43dbf-5ecf-405d-9a40-45325af72c7c" />
<img width="474" alt="04" src="https://github.com/user-attachments/assets/b3aa3500-d0b0-4c16-b03f-2cac558b25e2" />

4. En **Configuración de supervisión**, dejar Regla de recopilación de datos por defecto (puedes crear una nueva personalizada) > Configurar
<img width="485" alt="05" src="https://github.com/user-attachments/assets/b1057e63-813d-4a26-80dd-960f1a0dc8b1" />

5. Una Vez terminada la impementación, ingresa nuevamente a la VM, **Supervisión** > **Alertas**, selecciona **Ver y configurar**
<img width="784" alt="07" src="https://github.com/user-attachments/assets/eeffd755-07e7-4fc6-a3e9-b752c750b23b" />

6. En **Configuración de reglas de alertas recomendadas** activa el switch de **Percentage CPU es mayor que** dejando el limite en **80%**, En el apartado **Notificarme por** Selecciona **Correo elctrónico** y agrega un correo válido > Guardar
<img width="486" alt="08" src="https://github.com/user-attachments/assets/143da613-5fda-425e-a7e6-d290a3737fe9" />

## Tarea 2: Configurar Azure Backup

1. En **Azure Portal**, ingresa a **Almacenes de Recovery Services** > Crear
<img width="253" alt="09" src="https://github.com/user-attachments/assets/aee286f4-0fc8-471c-9f66-a13cfce4b639" />

2. Completa la información para crear un nuevo almacén de Recovery Services > Revisar y crear > Crear
<img width="442" alt="10" src="https://github.com/user-attachments/assets/3dbc6dba-d8a4-419e-a076-3ab5d96c2603" />

3. Ingresa al nuevo almacén de Recovery Services creado, dirígete a **Administrar** > **Directivas de backup** y selecciona **+ Agregar**
<img width="396" alt="11" src="https://github.com/user-attachments/assets/c7445e55-f3b8-4e96-b8bd-657e43413d35" />

4. En Tipo de directiva, selecciona Máquina virtual de Azure
<img width="335" alt="12" src="https://github.com/user-attachments/assets/c3ead169-6613-4d34-bbba-460bdef80b40" />

5. En Subtipo de directiva, seleccionar lo que mas se acomode al requerimiento, para este ejercico se utilizara **Mejorado**, Agrega un nombre a la directiva  y programa la copia de seguridad con una frecuencia **Diaria**, configura la **Retención de punto de copia de seguridad diario** para 7 días > Crear
<img width="659" alt="13" src="https://github.com/user-attachments/assets/c65aec5b-3b73-485c-94f0-fc357da728ae" />
<img width="555" alt="14" src="https://github.com/user-attachments/assets/9c466489-5b1c-406d-a78a-77d57363b401" />

6. Una vez creada la directiva, para realizar un respaldo manual de la VM, ingresar nuevamente al almacén y dirigirse a **Introducción** > **Copia de seguridad**, en la Carga de tarbajo selecciona Azure y Máquina virtual, selecciona **Realizar copia de seguridad**
<img width="482" alt="15" src="https://github.com/user-attachments/assets/12cda184-b7c6-480f-be8f-2cd7eabdeae4" />

7. Selecciona la directiva creada anteriormente, en **Máquinas Virtuales** > **Añadir**, selecciona la máquina virtual > Aceptar > **Habilitar copia de seguridad**
<img width="606" alt="16" src="https://github.com/user-attachments/assets/8577a0c4-ea16-456f-9508-289e954a35ac" />
<img width="941" alt="17" src="https://github.com/user-attachments/assets/1cc8cfb6-b9f1-4968-b85d-f25f170dab48" />
<img width="820" alt="18" src="https://github.com/user-attachments/assets/cf914d3f-6ca8-48da-8c37-c8b77dbf32fa" />

8. Regresa al almacén, dirigete a **Elementos protegidos** > **Elementos de copia de seguridad** y selecciona Azure Virtual Machine
<img width="641" alt="19" src="https://github.com/user-attachments/assets/f92d9a80-bd82-4e2d-8b16-d4b22b0d2fc7" />

9. Presiona los tres puntos al final de donde aparece la máquina virtual, selecciona **Hacer copia de seguridad ahora**, se iniciara la copia de seguridad, puede tardar 20 minutos en realizarce, por lo que puedes pasar al siguiente punto por mientras y luego regresar
<img width="954" alt="20" src="https://github.com/user-attachments/assets/6a3118a8-f9a3-4310-8b35-2a4106856bfd" />
<img width="943" alt="20-1" src="https://github.com/user-attachments/assets/4f0d38f4-ae47-481b-90fa-66ef24d1af44" />

## Tarea 3: Implementar Azure Site Recovery

1. Dirigirse a la VM, ingresar a **Copia de seguridad y recuperación ante desastres** > **Recuperación ante desastres**, elegir una región de destino (en mi caso East US ya que todos los laboratorios son realizados en West US) > **Configuración avanzada**
<img width="831" alt="21-1" src="https://github.com/user-attachments/assets/d3c05c3f-f4fe-4630-b611-cf5fd0f11cbc" />

2. Revisar la configuración de destino de grupo de recursos y red virtual (modificar si se necesita) > **Revisar e inciar replicaión** > **Iniciar replicación**
<img width="643" alt="22-1" src="https://github.com/user-attachments/assets/cb4c267d-8270-4c39-98f1-6d18f75bd5a6" />
<img width="484" alt="23-1" src="https://github.com/user-attachments/assets/bb6f809e-fd23-416d-bd2c-9ce3a3a9ed46" />

>**Nota**: La configuración de la replicación puede tardar mas de 30 minutos en realizarce, la configuración habrá terminado cuando ingreses nuevamente a **Recuperación ante desastres** y los botóne de **Conmutación por error** y **Conmutación por error de prueba** ya se encuentren disponibles, tal como se veran en la imágen del proximo paso

3. Una vez terminada la replicación, se debe probar la **Conmutación por error de prueba**, en la VM ingresa a **Copia de seguridad y recuperación ante desastres** > **Recuperación ante desastres**, esta ventana ya no será igual a como se veía antes de configurar la replicación, presionar botón **Conmutación por error de prueba**
<img width="913" alt="24" src="https://github.com/user-attachments/assets/2c6dae74-5162-42f9-83bb-9dabd57ee1e4" />

4. En la Red virtual de Azure, seleccionar la red de la replicación > **Conmutación por error de prueba**
<img width="513" alt="25" src="https://github.com/user-attachments/assets/6ed0caf0-2039-4291-8afc-77cc577122f2" />

5. Para validar que la **Conmutación por error de prueba** fue realizada de forma correcta, en la ventana de **Recuperación ante desastres** solo estará activo el botón para lmpiar la conmutación, otra prueba es, ingresar a **Maquinas virtuales**, ahora aparece la máquina virtual de la replicación en la ubicación configurada
<img width="719" alt="26" src="https://github.com/user-attachments/assets/38aba321-ad38-4d3b-903d-10c0040bd246" />
<img width="734" alt="27" src="https://github.com/user-attachments/assets/c727103d-4d99-47f9-adab-2171909df3f2" />

6. Para terminar la prueba, ingresa a la VM original a **Copia de seguridad y recuperación ante desastres** > **Recuperación ante desastres**, selecciona el botón **Limpiar conmutación por error de prueba**, habilitar check **La prueba esta completa ...** > Aceptar 
<img width="682" alt="28" src="https://github.com/user-attachments/assets/6bc4d8eb-6589-4cb2-ba30-e9361026b4c5" />
<img width="370" alt="29" src="https://github.com/user-attachments/assets/457742b3-3b7d-4c77-925f-882f78132f9b" />

7. Para supervisar el estado de la replicación, en el **Potal de Azure**, ingresar a **Supervisar** > **Alertas** > **Crear**
<img width="252" alt="31" src="https://github.com/user-attachments/assets/ef0f6ba7-19c6-4ee2-b6b3-032e557b50ba" />
<img width="409" alt="32" src="https://github.com/user-attachments/assets/cb1e5fc4-ce84-4959-bdcc-86fdbc58c761" />

8. En **Ambito**, presionar **+ Seleccionar ambito** y elegir el almacen de Recovery Services creado en la recuperación ante desastres > **Condición**
<img width="947" alt="33" src="https://github.com/user-attachments/assets/eac3ce47-5e0f-470a-b63c-d5a6808a5cbd" />

9. En **Condición**, seleccionar la señal **Backup Health Events**, en la **Lógica de alerta**, seleccionar el umbral en estático y el resto de opciones como se ven en la imágen > **Acciones**
<img width="917" alt="34" src="https://github.com/user-attachments/assets/e07dad01-8aa5-4533-b5ea-04ce4d4457cc" />

10. En **Acciones** seleccionar la acciones según se requieran, para este ejemplo, se seleccionan **Usar acciones rápidas** y se configuran los nombres y la acción de enviar un correo electrónico > **Detalles**
    <img width="952" alt="35" src="https://github.com/user-attachments/assets/6a73c9b5-a405-42a7-880a-4f6ada3f8951" />

11. Agregar los detalles del Grupo de recursos, Gravedad y Nombre de la regla de alertas > Revisar y crear > Crear

## Tarea 4: Consultar registros en Azure Monitor

>**Nota**: Los ejercicios se pueden realizar en el Área de trabajo de Log Analytics que se crea por defecto, pero para hacer este ejercicio mas especifico, se creara una nueva Área de trabajo de Logs Analytics

1. En el **Portal de Azure**, ingresar a **Áreas de trabajo de Log Anlaytics**
<img width="255" alt="37" src="https://github.com/user-attachments/assets/30743de2-4939-45ae-98fa-dfca30d9dc79" />

2. Colocar la información de la nueva Área de trabajo de Log Analytics > Revisar y crear > Crear
<img width="434" alt="01" src="https://github.com/user-attachments/assets/0db81abf-64fb-4865-8ef4-435aefefb6be" />

3. En el **Portal de Azure**, ingresar a **Supervisar**
<img width="252" alt="31" src="https://github.com/user-attachments/assets/51c89bd3-d3b2-428b-ad63-03c1c694f7de" />

4. Dirigirse a **Configuración** > **Reglas de recopilación de datos** > **crear**
<img width="456" alt="02" src="https://github.com/user-attachments/assets/bd4b6ceb-b86f-428a-8852-7c260e7af8b4" />

5. Llenar la información de los aspectos básico de la regla de recopilación de datos > **Recursos**
<img width="478" alt="03" src="https://github.com/user-attachments/assets/e9949c5a-7d26-4ec3-82aa-18bad9d6b3d4" />

6. Seleccionar **+ Agregar recursos**, seleccioanr la VM > Aplicar > **Recopilar y entregar**
<img width="953" alt="04" src="https://github.com/user-attachments/assets/5055799f-00de-4782-bc6f-7d63b4586701" />

7. Seleccionar **+ Agregar origen de datos**
<img width="375" alt="05" src="https://github.com/user-attachments/assets/77e21ed6-d898-4c1b-90a0-376a7673671e" />

8. En el menú deplegable en **Tipos de origen de datos**, seleccionar **Contadores de rendimiento**, seleccionar los contadores de rendimiento que se necesiten > **Destino**
<img width="489" alt="06" src="https://github.com/user-attachments/assets/abda513f-f076-4dca-ba5a-ff70c5c9e8d9" />

9. Agregar la información del destino > **Agregar origen de datos** > **Revisar y crear** > **Crear**
<img width="474" alt="07" src="https://github.com/user-attachments/assets/52f4b900-3fbe-449f-8dca-264305cc953b" />
<img width="447" alt="08" src="https://github.com/user-attachments/assets/fe353b37-ecd3-4c38-9930-071fce25e492" />

10. Ingresar al **Área de trabajo de Log Analytics** y seleccionar **Registros**
<img width="174" alt="09" src="https://github.com/user-attachments/assets/068df2ba-1d94-47b4-bb12-f4fad59bc898" />

11. Generar la consulta deseada
<img width="799" alt="13" src="https://github.com/user-attachments/assets/ce168ba2-0816-497b-bb7d-f65056a5a969" />



 

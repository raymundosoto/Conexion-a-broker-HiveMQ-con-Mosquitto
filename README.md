# Conexion-a-broker-HiveMQ-con-Mosquitto
Se detallan los pasos para hacer una conexión con el broker HiveMQ https://www.hivemq.com/

1. Usar linux en Ubunto 22 de preferencia
2. Instalar Mosquitto en una terminal con 
	sudo apt-add-repository ppa:mosquitto-dev/mosquitto-ppa
  	sudo apt-get update
	sudo apt install mosquitto
  - O ingresar a https://mosquitto.org/download/ para instalar
- Se puede instalar desde el repositorio de software de Ubuntu
- 
![imagen](https://user-images.githubusercontent.com/72757419/183270035-dfee055e-7cea-4c32-bd3f-5874068e01a3.png)
3. Comprobar que funciona mosquitto on 
-netstat -an
	(si no esta instalado, seguir las instrucciones sugeridas por la terminal para instalarlo)
	-Esperamos ver un servicio escuchando en el puerto 1883
  ![imagen](https://user-images.githubusercontent.com/72757419/183270202-d11e3e6b-c014-4163-ae18-52cf85003011.png)

4. Generar una suscripcion a Mosquitto usando broker público (se puede de forma local con localhost en la IP)

  - Conocer la IP del broker usando una nueva terminal en Ubuntu usando 
     nslookup broker.hivemq.com
     
     De aquí necesitamos el la ip que esté disponible ese día por ejemplo: 18.195.236.18

     ![imagen](https://user-images.githubusercontent.com/72757419/183270268-bba581c6-f4c6-42eb-acea-aa33a9a4f40f.png)
     
   - Crear un suscriptor usando 
   
   > mosquitto_sub -h 18.195.236.18 -p 1883 -q 0 -i raymundo_ss -t testtopic/hola_todos
    
      - Usar IP del broker
      - Usar el nombre_suscriptor adecuado (se puede cambiar)
      - Inscribirse al tópico adecuado para leer mensajes topico/topico_1
      Se verán los mensajes del tópico
      
      ![imagen](https://user-images.githubusercontent.com/72757419/183270420-55967bca-4fe1-46fc-a430-021c5e1dbcd6.png)

      
 5.  Hacer un publicador para enviarse mensajes al broker en el tópico adecuado
  - Crear un publicador usando
	> mosquitto_pub -h 18.195.236.18 -p 1883 -q 0 -i raymundo_ss -t testtopic/hola_todos -m "Hola grupo "
  
      - Usar IP del broker
      - Usar el nombre_suscriptor adecuado (se puede cambiar)
      - Inscribirse al tópico adecuado para leer mensajes topico/topico_1
      - Escribir el mensaje -m
      
      ![imagen](https://user-images.githubusercontent.com/72757419/183270469-4f1d72ea-5ef9-4fe3-863f-bc81eb5ad3df.png)
      
  Con lo anterior ya estaremos publicando en el broker y además leyendo los mensajes en la terminal
  
  6. Para hacerlo de forma local sólo hay que cambiar a localhost y quitar el suscriptor
  
  mosquitto_sub -h localhost -p 1883 -q 0 -t testtopic/hola_todo
  mosquitto_pub -h localhost -p 1883 -q 0 -i raymundo_ss -t testtopic/hola_todos -m "Hola grupo"
  
  ![imagen](https://user-images.githubusercontent.com/72757419/183270669-f9fdbf0d-0caf-4d45-b3ca-b36faa7f3915.png)
  
  :)


  






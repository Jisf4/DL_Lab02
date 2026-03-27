# Implementación de YOGA para detección de objetos

El presente repositorio cuenta con la implementación de YOGA, un modelo ligero para detección de objetos, de acuerdo a lo presentado en https://arxiv.org/abs/2307.05945.

Pasos para el entrenamiento:

1. Clonar este repositorio
   
Descargue el repositorio mediante el link o con el uso de `git clone` en la terminal de su preferencia.

2. Crear un entorno de Python con versión 3.9

   Puede crear el entorno para el código usando conda con el siguiente código:
   ```
   conda create -n YOGA python=3.9
   conda activate YOGA
   ```
3. Descargar las librerías necesarias
   Utilice las siguientes líneas de código para descargar las librerías de python:
   ```bash
   cd directorio_donde_descargó_el_repositorio
   pip install -r requirements.txt
   ```
4. Entrenamiento

   Antes de reallizar el entrenamiento, se debe modificar el archivo en ./models/yoga.yaml.
   ```
   nc: 10 # Número de clases de acuerdo a cada dataset
   ```
   Para realizar el entrenamiento utilice el siguiente comando:
   ```
   python train.py --img 640 --batch 16 --epochs 2 --data data/voc.yaml --cfg models/yoga.yaml --weights '' --device 0 --label-smoothing 0.1 --workers 2 --name yoga_voc_test
   ```
  Tener en cuenta el tamaño de batch, la cantidad de epochs, la ubicación de la base de datos que se quiere utilizar (data/....), el dispositivo (0 para GPU), el número de trabajadores y el nombre con el que desea guardar los resultados. Al realizar la selección de la base de datos que se desea utilizar, esta se descargará automáticamente en caso de que no cuente con ella.

  NOTA:
  En caso de error de detección de GPU, verificar que se ha instalado la versión adecuada de torch. Si no ha sido así se puede solucionar con el código proporcionado en https://pytorch.org/get-started/locally/.

  ```
  # Ejemplo
  pip uninstall torch torchvision torchaudio -y
  pip3 install torch torchvision --index-url https://download.pytorch.org/whl/cu126
  ```
  Se debe configurar la url de descarga en la página suministrada de acuerdo a las características de su computadora.

5. Resultados
   Los resultados van a ser guardados en ./runs/train/nombre_del_experimento

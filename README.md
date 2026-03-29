# Implementación de YOGA para detección de objetos

El presente repositorio cuenta con la implementación de YOGA, un modelo ligero para detección de objetos, de acuerdo a lo presentado en [YOGA: Deep Object Detection in the Wild with Lightweight Feature Learning and Multiscale Attention](https://arxiv.org/abs/2307.05945).

## Modificaciones realizadas a YOLO

- Creación de una nueva configuración en /models/yoga.yaml que incluye la arquitectura presentada en el artículo.
- Modificación del archivo /models/common.py para agregar los nuevos bloques: CSPGhost, MSCAM y AFF. Las modificaciones se encuentran al final del código.
- Modificación del archivo /models/yolo.py para incluir las reglas asociadas a los nuevos bloques. Se encuentran a partir de la línea 392 del código.
- Creación de un nuevo archivo de configuración para el dataset BDD100k en /data/bdd100k.yaml. El dataset modificado se puede descargar en el siguiente [link](https://drive.google.com/file/d/1w2cj7jSv4AlaZpRyxdbiLnXSwmrKZ23x/view?usp=sharing).
- Inclusión de resultados obtenidos para el entrenamiento de 3 bases de datos: PascalVOC, VisDrone y BDD100k


## Pasos para el entrenamiento de YOGA

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
  En caso de error de detección de GPU, verificar que se ha instalado la versión adecuada de torch. Si no ha sido así se puede solucionar con el código proporcionado en la página oficial de [Pytorch](https://pytorch.org/get-started/locally/).

  ```
  # Ejemplo
  pip uninstall torch torchvision torchaudio -y
  pip3 install torch torchvision --index-url https://download.pytorch.org/whl/cu126
  ```
  Se debe configurar la url de descarga en la página suministrada de acuerdo a las características de su computadora.

5. Resultados
   Los resultados van a ser guardados en ./runs/train/nombre_del_experimento

## Entrenamiento con Jetson Nano

Se pueden encontrar los resultados del entrenamiento en Jetson nano en la carpeta runs/Detect

## Trabajo basado en:

Sunkara, R., & Luo, T. (2023). YOGA: Deep object detection in the wild with lightweight feature learning and multiscale attention. Pattern Recognition, 139, 109451.

## 📜 License

Ultralytics provides two licensing options to meet different needs:

- **AGPL-3.0 License**: An [OSI-approved](https://opensource.org/license/agpl-v3) open-source license ideal for academic research, personal projects, and testing. It promotes open collaboration and knowledge sharing. See the [LICENSE](https://github.com/ultralytics/yolov5/blob/master/LICENSE) file for details.
- **Enterprise License**: Tailored for commercial applications, this license allows seamless integration of Ultralytics software and AI models into commercial products and services, bypassing the open-source requirements of AGPL-3.0. For commercial use cases, please contact us via [Ultralytics Licensing](https://www.ultralytics.com/license).


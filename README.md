#  Notas

App desarrollada para funcionar como template para poder inferir imágenes utilizando un modelo a través de COREML.
Las imágenes pueden ser cargadas desde la librería del dispositivo o pueden ser tomadas medianten  la cámara.
Inicialmente esta app incluye un modelo que permite inferir imágenes de flores: daisy, dandelion, roses, sunflowers y tulips.
El modelo utilizado fue generado mediante el siguiente tfcoreml (https://github.com/tf-coreml/tf-coreml ).
Luego de la instalación que se explica en el link, se generó el siguiente script para poder realizar la conversión a CoreML:

```
import tfcoreml as tf_converter
tf_converter.convert(tf_model_path = 'tf_files/retrained_graph.pb',
                        mlmodel_path = 'flowers.mlmodel',
                        image_input_names = 'input:0',
                        class_labels = 'tf_files/retrained_labels.txt',
                        output_feature_names = ['final_result:0'],
                        red_bias = -1,
                        green_bias = -1,
                        blue_bias = -1,
                        image_scale = 2.0/255.0)    
```


Para poder determinar el *output_feature_names* se utilizó el script inspect_pb.py que viene incluido en tfcoreml y además se incluye dentro de los fuentes de esta app.
```
python3 inspect_pb.py tf_files/retrained_graph.pb text_summary.txt
```
En el archivo generado (text_summary.txt) se debe buscar Softmax para poder deterinar el parámetro a enviar.




# Uso del modelo CLIPVision para procesar imágenes y generar incrustaciones de imágenes con Phi-3-vision

El siguiente ejemplo en python proporciona la funcionalidad necesaria para procesar imágenes y generar incrustaciones de imágenes usando el modelo CLIPVision.

## ¿Qué es CLIP?
CLIP, que significa Pre-entrenamiento Contrastivo de Lenguaje-Imagen, es un modelo desarrollado por OpenAI que aprende eficientemente conceptos visuales a partir de supervisión de lenguaje natural. Es un modelo multimodal que combina la comprensión de imágenes y texto en un solo marco. CLIP está entrenado en una variedad de imágenes obtenidas de internet y el texto encontrado con ellas, aprendiendo a predecir qué imágenes estaban emparejadas con qué textos, vinculando efectivamente las dos modalidades.

El modelo funciona tomando una imagen y un fragmento de texto como entrada y luego prediciendo la probabilidad de que el texto sea una descripción precisa de la imagen. Este enfoque permite que CLIP maneje una amplia gama de tareas visuales, como el reconocimiento de objetos, la clasificación e incluso la generación de descripciones para imágenes que nunca ha visto antes.

Una de las principales ventajas de CLIP es su capacidad para realizar aprendizaje "zero-shot", donde el modelo puede manejar correctamente tareas para las que no fue entrenado explícitamente, simplemente leyendo la descripción de la tarea. Esto es posible debido a la gran cantidad de datos diversos en los que ha sido entrenado, lo que le ayuda a generalizar bien a nuevas tareas.

## Phi-3-vision
Phi-3-vision es un modelo multimodal de 4.2B parámetros con capacidades de lenguaje y visión, capaz de razonar sobre imágenes del mundo real y documentos digitales, extrayendo y razonando sobre texto de imágenes, y generando ideas y respuestas relacionadas con gráficos o diagramas.

**Propósito del Ejemplo:** Este ejemplo demuestra cómo generar incrustaciones de imágenes usando CLIP y cómo puede aplicarse a tareas relacionadas con el modelo Phi-3. Sirve como referencia para comparar el rendimiento y las características de diferentes técnicas de incrustación (CLIP vs. Phi-3).
**Desafío de Integración:** Integrar otro codificador de visión como CLIP directamente en Phi-3 es realmente complejo. Esta complejidad surge debido a diferencias arquitectónicas y la necesidad de una integración sin problemas sin perder contexto o rendimiento. La integración aún no ha sido completamente evaluada o implementada, por lo que se incluye.
**Enfoque de Comparación:** El código tiene como objetivo proporcionar una comparación paralela en lugar de una solución integrada. Permite a los usuarios ver cómo funcionan las incrustaciones de CLIP junto con las incrustaciones de Phi-3, proporcionando información sobre los posibles beneficios o desventajas.
**Aclaración:** Este Ejemplo del Phi-3CookBook: Muestra cómo usar las incrustaciones de CLIP como una herramienta comparativa en lugar de una integración directa en Phi-3.
**Trabajo de Integración:** La integración completa de las incrustaciones de CLIP en Phi-3 sigue siendo un desafío y no se ha explorado completamente, pero está ahí para que los clientes experimenten.

## Código de Ejemplo
Este código define una clase llamada Phi3ImageEmbedding que representa un modelo de incrustación de imágenes. El propósito de esta clase es procesar imágenes y generar incrustaciones que pueden ser usadas para tareas posteriores como la clasificación o recuperación de imágenes.

El método __init__ inicializa el modelo configurando varios componentes como la eliminación de incrustaciones, el procesador de imágenes, los parámetros de transformación HD y la proyección de imágenes. Toma un objeto de configuración como entrada, que contiene parámetros de configuración para el modelo. El parámetro wte es una entrada opcional que representa incrustaciones de tokens de palabras.

El método get_img_features toma un tensor de entrada img_embeds que representa las incrustaciones de imágenes y devuelve un tensor que representa las características de imagen extraídas. Utiliza el img_processor para procesar las incrustaciones de imágenes y extraer las características deseadas basadas en los parámetros layer_idx y type_feature.

## Explicación del Código
Vamos a recorrer el código paso a paso:

El código importa las bibliotecas y módulos necesarios, incluyendo math, torch, torch.nn, y varios componentes de la biblioteca transformers.

El código define un objeto de configuración llamado CLIP_VIT_LARGE_PATCH14_336_CONFIG que contiene varios hiperparámetros para el modelo de incrustación de imágenes.

Se define la clase Phi3ImageEmbedding, que es una subclase de torch.nn.Module. Esta clase representa el modelo de incrustación de imágenes y contiene métodos para la propagación hacia adelante y la configuración de características de imagen.

El método __init__ inicializa el objeto Phi3ImageEmbedding. Toma un objeto de configuración como entrada, que es una instancia de la clase PretrainedConfig. También toma un argumento opcional wte.

El método __init__ inicializa varios atributos del objeto Phi3ImageEmbedding basado en el objeto de configuración proporcionado. Configura el tamaño oculto, la tasa de eliminación, el procesador de imágenes, la proyección de imágenes y otros parámetros.

El método set_img_features establece las características de imagen para el modelo. Toma un tensor de características de imagen como entrada y lo asigna al atributo img_features del objeto.

El método set_img_sizes establece los tamaños de imagen para el modelo. Toma un tensor de tamaños de imagen como entrada y lo asigna al atributo img_sizes del objeto.

El método get_img_features extrae características de imagen de las incrustaciones de imagen de entrada. Toma un tensor de incrustaciones de imagen como entrada y devuelve las características de imagen extraídas.

El método forward realiza la propagación hacia adelante a través del modelo. Toma IDs de entrada, valores de píxeles y tamaños de imagen como entrada y devuelve los estados ocultos del modelo. Primero verifica si las características de imagen y los tamaños ya están establecidos, y si no, utiliza la entrada proporcionada para configurarlos. Luego, procesa los IDs de entrada y extrae características de imagen basadas en el procesador de imágenes configurado. Finalmente, aplica la proyección de imágenes a las características extraídas y devuelve los estados ocultos.

En general, este código define una clase que representa un modelo de incrustación de imágenes y proporciona métodos para configurar características de imagen y realizar la propagación hacia adelante.

[Ejemplo de Código](../../../../code/06.E2E/phi3imageembedding.py)
```
import math
import torch
from transformers import CLIPVisionModel, PretrainedConfig
from transformers import CLIPVisionConfig 
from transformers.utils import logging
from datetime import datetime 

# Import necessary libraries
import torch.nn as nn

# Set up logging
logger = logging.get_logger(__name__)

# Define the configuration for the CLIPVisionModel
CLIP_VIT_LARGE_PATCH14_336_CONFIG = CLIPVisionConfig(
    attention_dropout=0.0,
    dropout=0.0,
    hidden_act="quick_gelu",
    hidden_size=1024,
    image_size=336,
    initializer_factor=1.0,
    initializer_range=0.02,
    intermediate_size=4096,
    layer_norm_eps=1e-05,
    num_attention_heads=16,
    num_channels=3,
    num_hidden_layers=24,
    patch_size=14,
    projection_dim=768 
)

# Define the Phi3ImageEmbedding class
class Phi3ImageEmbedding(nn.Module):
        """Phi3 Image embedding."""

        def __init__(self, config: PretrainedConfig, wte=None, **kwargs) -> None:
                super().__init__()

                # Set up the embedding dropout
                hidden_size = config.n_embd if hasattr(config, 'n_embd') else config.hidden_size
                if hasattr(config, 'embd_pdrop') or hasattr(config, 'embed_pdrop'):
                        embd_drop = config.embd_pdrop if hasattr(config, 'embd_pdrop') else config.embed_pdrop
                        self.drop = nn.Dropout(embd_drop)
                else:
                        self.drop = None

                self.wte = wte

                # Set up the image processor based on the configuration
                if isinstance(config.img_processor, dict) and config.img_processor.get('name', None) == 'clip_vision_model':
                        assert 'model_name' in config.img_processor, 'model_name must be provided for CLIPVisionModel'
                        assert 'image_dim_out' in config.img_processor, 'image_dim_out must be provided for CLIPVisionModel'
                        assert 'num_img_tokens' in config.img_processor, 'num_img_tokens must be provided for CLIPVisionModel'
                        assert config.img_processor['model_name'] == 'openai/clip-vit-large-patch14-336'
                        clip_config = CLIP_VIT_LARGE_PATCH14_336_CONFIG
                        self.img_processor = CLIPVisionModel(clip_config)
                        image_dim_out = config.img_processor['image_dim_out']
                        self.num_img_tokens = config.img_processor['num_img_tokens']
                else:
                        raise NotImplementedError(f'img_processor = {config.img_processor}, not implemented')

                self.image_dim_out = image_dim_out
                self.img_sizes = None

                # Set up the HD transform parameters
                self.use_hd_transform = kwargs.get('use_hd_transform', False)
                self.with_learnable_separator = kwargs.get('with_learnable_separator', False)
                self.hd_transform_order = kwargs.get('hd_transform_order', 'glb_sub')
                assert self.use_hd_transform == self.with_learnable_separator, 'use_hd_transform and with_learnable_separator should have same value'
                if self.with_learnable_separator:
                        assert self.use_hd_transform, 'learnable separator is only for hd transform'
                        self.glb_GN = nn.Parameter(torch.zeros([1, 1, self.image_dim_out * 4]))
                        self.sub_GN = nn.Parameter(torch.zeros([1, 1, 1, self.image_dim_out * 4]))
                        logger.info(f'learnable separator enabled for hd transform, hd_transform_order = {self.hd_transform_order}')

                # Set up the image projection based on the projection_cls
                projection_cls = kwargs.get('projection_cls', 'linear')
                if projection_cls == 'linear':
                        self.img_projection = nn.Linear(image_dim_out, hidden_size)
                elif projection_cls == 'mlp' and self.use_hd_transform:
                        dim_projection = hidden_size
                        depth = 2
                        layers = [nn.Linear(image_dim_out * 4, dim_projection)]
                        for _ in range(1, depth):
                                layers.extend([nn.GELU(),
                                                                nn.Linear(dim_projection, dim_projection)])
                        self.img_projection = nn.Sequential(*layers)
                elif projection_cls == 'mlp':
                        dim_projection = hidden_size
                        depth = 2
                        layers = [nn.Linear(image_dim_out, dim_projection)]
                        for _ in range(1, depth):
                                layers.extend([nn.GELU(),
                                                                nn.Linear(dim_projection, dim_projection)])
                        self.img_projection = nn.Sequential(*layers)
                else:
                        raise NotImplementedError(f'projection_cls = {projection_cls}, not implemented')

                self.vocab_size = config.vocab_size
                self.img_features = None

                # Set up the layer index and type of feature for the image processor
                if isinstance(config.img_processor, dict):
                        self.layer_idx = config.img_processor.get('layer_idx', -2)
                        self.type_feature = config.img_processor.get('type_feature', 'patch')
                else:
                        self.layer_idx = -2
                        self.type_feature = 'patch'


        def set_img_features(self, img_features: torch.FloatTensor) -> None:
                self.img_features = img_features

        def set_img_sizes(self, img_sizes: torch.LongTensor) -> None:
                self.img_sizes = img_sizes

        def get_img_features(self, img_embeds: torch.FloatTensor) -> torch.FloatTensor:
                LAYER_IDX = self.layer_idx
                TYPE_FEATURE = self.type_feature

                img_processor_output = self.img_processor(img_embeds, output_hidden_states=True)
                img_feature = img_processor_output.hidden_states[LAYER_IDX]

                if TYPE_FEATURE == "patch":
                        patch_feature = img_feature[:, 1:]
                        return patch_feature

                if TYPE_FEATURE == "cls_patch":
                        return img_feature

                raise NotImplementedError

        def forward(self, input_ids: torch.LongTensor, pixel_values: torch.FloatTensor, image_sizes=None) -> torch.FloatTensor:

                MAX_INPUT_ID = int(1e9)
                img_embeds = pixel_values
                img_sizes = image_sizes

                if self.img_features is not None:
                        img_embeds = self.img_features.clone()
                        self.img_features = None

                if self.img_sizes is not None:
                        img_sizes = self.img_sizes

                input_shape = input_ids.size()
                input_ids = input_ids.view(-1, input_shape[-1])

                with torch.no_grad():
                        positions = torch.nonzero((input_ids < 0) & (input_ids > -MAX_INPUT_ID), as_tuple=False)
                
                select = False

                if isinstance(self.img_projection, nn.Sequential):  
                        target_device = self.img_projection[0].bias.device  
                        target_dtype = self.img_projection[0].bias.dtype  
                else:  # It's a single nn.Linear layer  
                        target_device = self.img_projection.bias.device  
                        target_dtype = self.img_projection.bias.dtype  

                if len(positions.tolist()) > 0:
                        with torch.no_grad():
                                g_values = abs(input_ids[positions[:, 0], positions[:, 1]])

                        if self.use_hd_transform and img_sizes is not None and len(img_sizes):
                                hd_transform = True
                                assert img_embeds.ndim == 5, f'img_embeds size: {img_embeds.size()}, expect 5D tensor for hd transform'
                                img_features = self.get_img_features(img_embeds.flatten(0, 1))
                                base_feat_height = base_feat_width = int(img_features.shape[1] ** 0.5)
                                assert base_feat_height == 24 and base_feat_width == 24, f'base_feat_height: {base_feat_height}, base_feat_width: {base_feat_width}, expect 24x24 features for hd transform'
                                img_features = img_features.view(bs, -1, base_feat_height * base_feat_width, self.image_dim_out)
                                C = self.image_dim_out
                                H = base_feat_height

                                output_imgs = []
                                output_len = []
                                if isinstance(img_sizes, torch.Tensor):
                                        img_sizes = img_sizes.view(-1, 2)
                                for _bs in range(bs):
                                        h, w = img_sizes[_bs]
                                        h = h // 336 
                                        w = w // 336
                                        B_ = h * w

                                        global_img_feature = img_features[_bs, :1]
                                        glb_img = global_img_feature.reshape(1,H,H,C).reshape(1,H//2,2,H//2,2,C).contiguous().permute(0,1,3,2,4,5).reshape(1,H//2,H//2,4*C).contiguous()
                                        temp_glb_GN = self.sub_GN.repeat(1, H//2, 1, 1)
                                        glb_img = torch.cat([glb_img, temp_glb_GN], dim=2).reshape(1,-1,4*C)
                                        sub_img = img_features[_bs, 1:]
                                        sub_img = sub_img[:B_]
                                        sub_img = sub_img.reshape(B_,H,H,C).reshape(B_,H//2,2,H//2,2,C).contiguous().permute(0,1,3,2,4,5).reshape(B_,-1,4*C).contiguous()
                                        sub_img = sub_img.reshape(1, h, w, 12, 12, -1).permute(0,1,3,2,4,5).reshape(1,h*12,w*12,4*C)
                                        temp_sub_GN = self.sub_GN.repeat(1, h*12, 1, 1)
                                        sub_img = torch.cat([sub_img, temp_sub_GN], dim=2).reshape(1,-1,4*C)
                                        if self.hd_transform_order == 'glb_sub':
                                                output_imgs.append(torch.cat([glb_img, self.glb_GN, sub_img], dim=1))
                                        elif self.hd_transform_order == 'sub_glb':
                                                output_imgs.append(torch.cat([sub_img, self.glb_GN, glb_img], dim=1))
                                        else:
                                                raise NotImplementedError(f'hd_transform_order = {self.hd_transform_order}, not implemented')
                                        temp_len = int((h*w+1)*144 + 1 + (h+1)*12)
                                        assert temp_len == output_imgs[-1].shape[1], f'temp_len: {temp_len}, output_imgs[-1].shape[1]: {output_imgs[-1].shape[1]}'
                                        output_len.append(temp_len)
                                
                                num_img_tokens = output_len
                                img_set_tensor = []
                                for _output_img in output_imgs:
                                        img_feature_proj = self.img_projection(_output_img.to(target_device).to(target_dtype))
                                        img_set_tensor.append(img_feature_proj)
                                logger.info(f'img_embeds size: {img_embeds.size()}, image sizes: {img_sizes} loading time {datetime.now() - start_time}')
                        elif img_embeds.ndim == 4:
                                selected_g_values = g_values[::self.num_img_tokens]
                                assert len(img_embeds) == len(selected_g_values), f'img_embeds size: {img_embeds.size()}, selected_g_values size: {len(selected_g_values)}, selected_g_value {selected_g_values}'
                                start_time = datetime.now()
                                tt = (
                                        self.get_img_features(img_embeds)
                                        .to(target_device)
                                        .to(target_dtype)
                                        .reshape(-1, self.image_dim_out)
                                )
                                logger.info(f'img_embeds size: {img_embeds.size()}, loading time {datetime.now() - start_time}')
                                img_set_tensor = self.img_projection(tt)
                        elif img_embeds.ndim == 3:
                                selected_g_values = g_values[::self.num_img_tokens]
                                assert len(img_embeds) == len(selected_g_values), f'img_embeds size: {img_embeds.size()}, selected_g_values size: {len(selected_g_values)}, selected_g_value {selected_g_values}'
                                tt = (
                                        img_embeds
                                        .to(target_device)
                                        .to(target_dtype)
                                        .view(-1, self.image_dim_out)
                                )
                                img_set_tensor = self.img_projection(tt)
                        else:
                                raise NotImplementedError
                        select = True
                
                with torch.no_grad():
                        input_ids.clamp_min_(0).clamp_max_(self.vocab_size)
                
                hidden_states = self.wte(input_ids)

                if select:
                        if hd_transform:
                                idx = 0
                                for i, cnt in enumerate(num_img_tokens):
                                        hidden_states[positions[idx, 0], positions[idx, 1] : positions[idx, 1] + cnt] = (
                                                img_set_tensor[i]
                                                .to(hidden_states.dtype)
                                                .to(hidden_states.device)
                                                )
                                        idx += cnt
                        else:
                                idx = 0
                                assert len(selected_g_values) * self.num_img_tokens == len(img_set_tensor), f'len(selected_g_values) * self.num_img_tokens = {len(selected_g_values) * self.num_img_tokens}, len(img_set_tensor) = {len(img_set_tensor)}'
                                for i, g in enumerate(selected_g_values):
                                        cnt = self.num_img_tokens
                                        hidden_states[positions[idx, 0], positions[idx, 1] : positions[idx, 1] + cnt] = (
                                                img_set_tensor[i * cnt : (i + 1) * cnt]
                                                .to(hidden_states.dtype)
                                                .to(hidden_states.device)
                                                )
                                        idx += cnt

                if self.drop is not None:
                        hidden_states = self.drop(hidden_states)

                return hidden_states
```

## Construyendo tu Pipeline

Trabajando con código que genera incrustaciones, como el ejemplo anterior, normalmente lo integras en tu pipeline dependiendo de tu caso de uso específico.

1. Cargando Modelos Pre-entrenados: Si estás cargando modelos pre-entrenados de Hugging Face, estos modelos son en efecto binarios. Puedes usarlos directamente para generar incrustaciones sin entrenamiento adicional. Esto es útil para tareas como extracción de características o búsqueda semántica donde necesitas incrustaciones listas para usar.

2. Pipeline de Ajuste Fino: Si necesitas adaptar el modelo a una tarea o conjunto de datos específico, integrarías el código en un pipeline de ajuste fino. Esto implica:
   - Cargar el Modelo Pre-entrenado: Comienza con un modelo pre-entrenado de Hugging Face.
   - Preparar tu Conjunto de Datos: Asegúrate de que tu conjunto de datos esté en el formato correcto para el entrenamiento.
   - Ajuste Fino: Usa bibliotecas como `transformers` and `datasets` de Hugging Face para ajustar el modelo en tu conjunto de datos. Este paso ajusta los pesos del modelo para adaptarse mejor a tu tarea específica.

Por ejemplo, en el contexto del Phi-3 Cookbook y CLIPVision, podrías:
- Generar Incrustaciones: Usar el modelo CLIP pre-entrenado para generar incrustaciones para imágenes.
- Ajuste Fino: Si las incrustaciones necesitan ser más específicas para tu aplicación, ajusta finamente el modelo CLIP en un conjunto de datos relevante para tu caso de uso.

Aquí hay un ejemplo simplificado de cómo podrías integrar esto en el código:

```python
from transformers import CLIPProcessor, CLIPModel
import torch
 
# Load pre-trained model and processor
model = CLIPModel.from_pretrained("openai/clip-vit-base-patch32")
processor = CLIPProcessor.from_pretrained("openai/clip-vit-base-patch32")
 
# Prepare your data
images = [...]  # List of images
inputs = processor(images=images, return_tensors="pt")
 
# Generate embeddings
with torch.no_grad():
    embeddings = model.get_image_features(**inputs)
 
# Fine-tuning (if needed)
# Define your fine-tuning logic here
```

Este enfoque te permite aprovechar modelos pre-entrenados poderosos y adaptarlos a tus necesidades específicas.

## Integrando la Familia de Modelos Phi

Integrar el modelo Phi-3 con el ejemplo de código proporcionado que involucra CLIP puede ser un desafío, especialmente cuando se consideran diferentes codificadores de visión.

Aquí hay una breve descripción de cómo podrías abordar esto:

### Puntos Clave
**Procesamiento de Datos:** Asegúrate de que las imágenes se procesen de una manera que se ajuste a los requisitos de entrada del modelo Phi-3.
**Generación de Incrustaciones:** Reemplaza la generación de incrustaciones de CLIP con el método correspondiente de tu modelo Phi-3.
**Ajuste Fino:** Si necesitas ajustar finamente el modelo Phi-3, asegúrate de que la lógica esté incluida después de generar las incrustaciones.

## Pasos para Integrar el Modelo Phi-3
**Cargar el Modelo Phi-3:** Suponiendo que tienes una clase Phi3Model para el modelo Phi-3 estándar o ajustado finamente.
**Modificar la Preparación de Datos:** Ajusta la preparación de datos para adaptarse a los requisitos de entrada del modelo Phi-3.
**Integrar Incrustaciones de Phi-3:** Reemplaza la parte donde se generan las incrustaciones de CLIP con la generación de incrustaciones del modelo Phi-3.

```
from transformers import CLIPProcessor, CLIPModel
import torch
 
# Load pre-trained CLIP model and processor
clip_model = CLIPModel.from_pretrained("openai/clip-vit-base-patch32")
clip_processor = CLIPProcessor.from_pretrained("openai/clip-vit-base-patch32")
 
# Load Phi-3 model (vanilla or fine-tuned)
# Assuming you have a load_phi3_model function to load your Phi-3 model
phi3_model = load_phi3_model(fine_tuned=True)
 
# Prepare your data
images = [...]  # List of images
inputs = clip_processor(images=images, return_tensors="pt")
 
# Generate embeddings using CLIP (for comparison)
with torch.no_grad():
    clip_embeddings = clip_model.get_image_features(**inputs)
 
# Generate embeddings using Phi-3
# Adjust this part according to how your Phi-3 model processes inputs
phi3_inputs = process_for_phi3_model(images)
with torch.no_grad():
    phi3_embeddings = phi3_model.get_image_features(phi3_inputs)
 
# Fine-tuning or further processing (if needed)
# Define your fine-tuning logic here
``

        **Descargo de responsabilidad**: 
        Este documento ha sido traducido utilizando servicios de traducción automatizada por IA. Aunque nos esforzamos por lograr precisión, tenga en cuenta que las traducciones automáticas pueden contener errores o imprecisiones. El documento original en su idioma nativo debe considerarse la fuente autorizada. Para información crítica, se recomienda una traducción profesional humana. No somos responsables de ningún malentendido o interpretación errónea que surja del uso de esta traducción.
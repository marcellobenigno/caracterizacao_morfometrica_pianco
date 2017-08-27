## Recorte da área de interesse


Primeiramente importamos o shapefile da área de interesse:


![image](img/10.png)


![image](img/11.png)


Importada a área de estudo, podemos então definir a **region** a partir dela. Uma region no GRASS define a área de interesse e a resolução espacial da área de análise dos dados matriciais.


```
g.region -dp vector=ai

```

Convertemos então a área de estudo (vetorial) em uma camada raster:

```
v.to.rast input=ai output=ai.rst use=val value=1

```

Através de álgebra de mapas, extraímos da camada **mosaico_srtm_utm.tif** a área de estudo:

```
r.mapcalc "dem = mosaico_srtm_utm * ai.rst"

```

```
r.colors map=dem color=elevation
```

Por último, definimos a área de estudo novamente, a parte do srtm recortado (camada **dem**):

```
g.region -dp raster=dem res=90

```

[voltar para a metodologia][0]


[0]:metodologia.md



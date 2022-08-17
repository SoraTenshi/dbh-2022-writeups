# scrolling-video

Fuer diese Challenge haben wir eine Videodatei mit einem relativ kleinen Ausschnitt bekommen, in welchem die Flagge erkenntlich ist.

Zum loesen habe ich das Video in dessen Frames aufgeteilt, welches mit dem folgenden ffmpeg-command durchgefuehrt werden kann: `ffmpeg -i "./dings.mov" frames/03d.jpg`

Anschliessend habe ich ein kleines python script geschrieben (neija, eher aus dem internet geliehen :)), welches die frames horizontal aneinanderkettet.

```python
import sys
import os
from PIL import Image

f_f = "./frames"
images = []
for _,_,fs in os.walk(f_f):
    for f in fs:
      xd = '{}/{}'.format(f_f, f)
      print(xd)
      images.append(xd)
      
images.sort()
imgs = [ Image.open(x) for x in images]
w, h = zip(*(i.size for i in imgs))
t_w = sum(w)
t_h = sum(h)

n = Image.new('RGB', (t_w, t_h))
off = 0
for im in imgs:
  n.paste(im, (off, 0))
  off += im.size[0]
            
n.save('test.jpg')
```

Welches in die folgende Flagge resultierte: `DBH{W3R_A_S4GT_MU55_4UCH_GUSTAV_S4GEN}`

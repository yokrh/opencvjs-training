# OpenCV.js

https://docs.opencv.org/3.4.1/d6/d10/tutorial_js_root.html


## Setup

https://docs.opencv.org/3.4.1/d4/da1/tutorial_js_setup.html

```sh
# git clone https://github.com/opencv/opencv.git

# cd opencv/
# # python ./platforms/js/build/js.py build_js  # asm.js

# git clone https://github.com/emscripten/core/emsdk.git
# cd emsdk/
# ./emsdk install latest
# ./emsdk activate latest
# source ./emsdk_env.sh --build=Release
# cd ../
# export EMSCRIPTEN=$EMSDK
# python ./platforms/js/build_js.py build_wasm --build_wasm  # wasm
# # failed ?!?!?!?!??!?!?!
```

```sh
# curl -LO https://docs.opencv.org/3.4.1/opencv.js
curl -LO https://docs.opencv.org/4.0.1/opencv.js
```


## Hello world

https://docs.opencv.org/3.4.1/d0/d84/totorial_js_usage.html

```sh
mkdir hello-opencvjs && cd $_

cp ../opencv.js .
touch index.html
```

`index.html`
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello OpenCV.js</title>
</head>
<body>
  <h2>Hello OpenCV.js</h2>
  <p id="status">OpenCV.js is loading...</p>
  <div>
    <div class="inputoutput">
      <img id="imageSrc" alt="No Image">
      <div class="caption">imageSrc <input type="file" id="fileInput" name="file"></div>
    </div>
    <div class="inputoutput">
      <canvas id="canvasOutput"></canvas>
      <div class="caption">canvasOutput</div>
    </div>
  </div>

  <script type="text/javascript">
    let imgElement = document.getElementById('imageSrc');
    let inputElement = document.getElementById('fileInput');
    inputElement.addEventListener('change', (e) => {
      imgElement.src = URL.createObjectURL(e.target.files[0]);
    }, false);
    imgElement.onload = function() {
      let mat = cv.imread(imgElement);
      cv.imshow('canvasOutput', mat);
      mat.delete();  // neccesary. important.
    }
    function onOpenCvReady() {
      document.getElementById('status').innerHTML = 'OpenCV.js is ready.';
    }
  </script>
  <script async src="opencv.js" onload="onOpenCvReady();"></script>
</body>
</html>
```

```sh
python -m SimpleHTTPServer 8888
```

Access to http://localhost:8888/.
yeah!!!
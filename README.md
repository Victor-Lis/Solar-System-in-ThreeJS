
# Solar-System-Project

Esse é mais um projeto que faz parte dos meus estudos de ThreeJS, pois acredito que agregue bastante no Front-End. 

Dessa vez continuando a saga de vídeo do canal [WaelYasmina](https://www.youtube.com/channel/UC1q2FdkcQ4qIxXzj3KQ1HYA).

Vi um [vídeo](https://www.youtube.com/watch?v=XXzqSAt3UIw) sobre a criação de um Sistema Solar.

Curiosamente já tinha tentado fazer um no projeto ["FirstProject-ThreeJS"](https://github.com/Victor-Lis/FirstProject-ThreeJS), mas não tinha ficado tão bacana.
## Aprendizados

- Utilizar o TextureLoader;
- Trabalhar com diferentes Lights;
- Trabalhar com objetos 3D, para cada planeta ter rotação própria em torno do Sol;
- Criar uma função dinâmica para criar os planetas.
## Uso/Exemplos

### TextureLoader
Ele é o responsável por renderizar uma textura, por exemplo uma imagem, como no trecho abaixo
```javascript
const textureLoader = new THREE.TextureLoader()

const sunGeo = new THREE.SphereGeometry(16, 30, 30)
const sunMat = new THREE.MeshBasicMaterial({
    map: textureLoader.load(sunTexture) // Utilizando o textureLoader
})
const sun = new THREE.Mesh(sunGeo, sunMat)
scene.add(sun)
```

### Lights
No projeto foi utilizado 2 "lights" diferentes, a luz ambiente, para ser a ilumição do projeto como um todo e o ponto de luz, para simular a ilumição do Sol.
```js
const ambientLight = new THREE.AmbientLight(0x444444)
scene.add(ambientLight)

const pointLight = new THREE.PointLight(0xFFFFFF, 3500, 300)
scene.add(pointLight)
```

### Objeto 3D

De maneira resumida, pois no exemplo da função createPlanet(), vai ter um pouco mais sobre. 

Nesse projeto para cada planeta é criado um Objeto 3D respectivo, para simular a posição do sol e, sendo assim, ao modificar a rotação desse objeto 3D, irá influenciar a posição do seu "filho" o planeta. 
```js
const obj = new THREE.Object3D()
```

### Função createPlanet()
Essa é a função responsável pela criação dos planetas, ela como explicado acima cria um Objeto 3D para simular a posição do Sol e cria o planeta a partir dos parâmetros passados, que são "size", "texture" e "position" e opcionalmente "ring", para criar um anel entorno dele.

A função retorna um objeto com os atributos mesh e obj, sendo mesh o planeta em si e obj o Objeto 3D.

Segue abaixo a função em si e um exemplo de uso.

#### Função
```js
function createPlanet(size, texture, position, ring) {
    const geo = new THREE.SphereGeometry(size)
    const mat = new THREE.MeshStandardMaterial({
        map: textureLoader.load(texture)
    })
    const mesh = new THREE.Mesh(geo, mat)
    mesh.position.x = position
    const obj = new THREE.Object3D()
    obj.add(mesh)
    scene.add(obj)

    if(ring){
        const ringGeo = new THREE.RingGeometry(
            ring.innerRadius, 
            ring.outerRadius, 
            32
        )
        const ringMat = new THREE.MeshStandardMaterial({
            map: textureLoader.load(ring.texture),
            side: THREE.DoubleSide
        })
        const ringMesh = new THREE.Mesh(ringGeo, ringMat)
        obj.add(ringMesh)
        ringMesh.position.x = position
        ringMesh.rotation.x = -0.5 * Math.PI
    }

    return {mesh, obj}
}
```

#### Uso
```js
const earth = createPlanet(6, earthTexture, 62)
```

### Função animate()
Não é um aprendizado novo exatamente pois já há utilizei algumas vezes, mas não deixa de ser um desafio pois no caso trabalhei com os planetas criados a partir da função createPlanet()

```js
function animate() {
    
    // Self-Mesh Rotation
    sun.rotateY(0.004)
    mercury.mesh.rotateY(0.004)
    venus.mesh.rotateY(0.002)
    earth.mesh.rotateY(0.02)
    mars.mesh.rotateY(0.018)
    jupiter.mesh.rotateY(0.04)
    saturn.mesh.rotateY(0.038)
    uranus.mesh.rotateY(0.03)
    neptune.mesh.rotateY(0.032)
    pluto.mesh.rotateY(0.008)
    
    // Around-Sun Rotation
    mercury.obj.rotateY(0.04)
    venus.obj.rotateY(0.015)
    earth.obj.rotateY(0.01)
    mars.obj.rotateY(0.008)
    jupiter.obj.rotateY(0.002)
    saturn.obj.rotateY(0.0009)
    uranus.obj.rotateY(0.0004)
    neptune.obj.rotateY(0.0001)
    pluto.obj.rotateY(0.00007)

    renderer.render(scene, camera);
}
```
## Screenshots

![Screenshot1](https://github.com/Victor-Lis/Solar-System-in-ThreeJS/blob/master/ProjectImages/Screenshot1.png)

![Screenshot2](https://github.com/Victor-Lis/Solar-System-in-ThreeJS/blob/master/ProjectImages/Screenshot2.png)

![Screenshot3](https://github.com/Victor-Lis/Solar-System-in-ThreeJS/blob/master/ProjectImages/Screenshot3.png)

## Autores

- [@Victor-Lis](https://github.com/Victor-Lis)


# Framework
`application.cpp` is the most important
- Creates the scene + camera
- Mainly divided in render() and update() as in CA 
	- Update mainly for mouse control, render will be used a lot more 

`mesh.cpp`:
- Vertices 
`mat4`:
- Model matrix (all the informations)
`material.cpp`
- Standard material is a subclass of material, used to create specific types of materials
- `Material::Render` sends the information from the app to the shaders
```cpp
void FlatMaterial::render(Mesh* mesh, glm::mat4 model, Camera* camera)
{
	if (mesh && this->shader) {
		// Enable shader
		this->shader->enable();

		// Upload uniforms
		setUniforms(camera, model);

		// Do the draw call
		mesh->render(GL_TRIANGLES);

		this->shader->disable();
	}
}
```

`shader.cpp`
`texture.cpp`
# Shaders
```ad-note
`gl_FragColor` was deprecated some versions ago, we can simply use any `out vec4` variable and it will work
```
Applications use information from material, materials send parameters to shaders
Application render calls material render, which then renders the shaders

We can access application info from materials with `Application::instance->param`

```ad-missing
CREATE NEW MATERIAL AND FRAGMENT SHADER
```

# Tasks
## Extending framework to Absorption model for homogeneous volumes
For AABB intersection test, check the code in mesh.h
	glm::vec3 aabb_min; 
	glm::vec3 aabb_max;
	
Though since the box it's normalized we can hardcode it instead:


```ad-important
CAMERA IS IN GLOBAL, WE NEED IT IN LOCAL COORDINATES FOR THE SHADER TO WORK PROPERLY, WE SHOULD FOLLOW THE CODE ON THE SLIDES
```
```cpp
glm::mat4 inverseModel = glm::inverse(model)
glm::vec4 temp = ...
...
```

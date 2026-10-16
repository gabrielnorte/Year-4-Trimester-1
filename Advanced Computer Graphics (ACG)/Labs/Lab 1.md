# Framework:
- `shader.cpp:`
Parent class for all the other shaders, *Shaders are objects responsible for computing the light that travels along a given ray*
All the other shader classes extend from it, and are forced to define the `computeColor()` method, which returns the light intensity along a ray

SHADERS AND INTEGRATORS ARE THE SAME

- `intersectionshader.cpp`
Child shader of `shader.cpp`
`ComputeColor()` returns a certain color for the rays that intersect a scene object, and another color if no intersection is detected

- `pointlight.h`
Child of lights, they're just defined by position and intensity

- `material.cpp`
Parent class that will be used to implement the materials in the ray tracer. It forces
the derived classes to implement the getReflectance() method which, given the normal n, the direction ωi and the direction ωo, returns the light arriving from ωi reflected in the direction ωo

- `ray.cpp`
This class is in charge of defining the ray and its properties.
	Characterized by **origin** and **direction**
	Also `Tmin` and `Tmax` information, indicating the section of the ray that interects the object s


HDR images don't clamp to 1, it extends up to a 100, meaning, we have more "white tones"
- Normal images in lab1 will clamp to one though

## Task 2
`raytrace()` will generate the image
- The color will be determined by the color at `intersectionshader`

## Contents 
**Task 1:**
```cpp
Vector3D IntersectionShader::computeColor(const Ray &r, const std::vector<Shape*> &objList, const std::vector<LightSource*> &lsList) const
{

    //for (int i = 0; i < objList.size(); i++) {
    //    if (objList.at(i)->rayIntersectP(r)) return Vector3D(1.0, 0.0, 0.0);
    //}

    // TASK 2 --------
    // This if is only entered for certain pixels
	    if (Utils::hasIntersection(r, objList)) //Checks if there's an intersection with the ray and the list of objects
        return Vector3D(0.0, 1.0, 0.0);

    //Both return but they affect different pixels
    return bgColor;
}
```
**Task 2:**

**Task 3:**
This should be moved to IntersectionDepthShader.cpp
```cpp
    Intersection its;
    //Even though this is an empty class, it will be modified within getClosestIntersection()

    if (Utils::getClosestIntersection(r, objList, its)) {
        Vector3D intersection_pos = its.itsPoint; // Get intersection point
        Vector3D camera_origin = r.o; // The camera is the origin of the ray

        float distance = (r.o - intersection_pos).length(); //Normalize

        return Vector3D(0,1.0 - distance/10.0, 0.0); //More intense color based on distance
    }
```

# Materials
They model the way light is reflected with the object with this material. Depends on:
- Viewing direction
- The normal at the position $x$
- Incident light direction

This behavior is captured by Bidirectional Reflectance Distribution Function (DRDF)

All the materials (mirror, phong and tramission) inherit from material, but some functions are set based on their behavior
- `GetRefractiveIndex`: Is not defined for non-transmissive materials, meanwhile for transmissive it returns `ut` ($u_{T} = \eta_{2}/\eta_{1}$)
## Phong
A Phong BRDF uses coefficients $p_{d}$ (diffuse, default material color), $k_{s}$ (specular color) and $\alpha$ (shininess coefficient).
We define $w_{r}$ as the ideal reflection direction
# Utils
`get_closest_intersection(const Ray& camera_ray, vector<Shape>& objects_list, Intersection its)`

- Intersection is passed on as an empty instance, that gets completed once an intersection is found

```cpp

    bool hasIntersection = false;

    for (size_t objIndex = 0; objIndex < objectsList.size(); objIndex++)
    {
        // Get the current object
        const Shape* obj = objectsList.at(objIndex); //Store object as shape
        if (obj->rayIntersect(cameraRay, its)) //Executing rayIntersect() completes missing arguments from empty Intersection instance
            hasIntersection =  true;
    }
    return hasIntersection;
```


```
BassPess.fp


#version 140
precision highp float;

// 7a. Create input channel through which texture coordinates will be received from vertex shader
// ...
in vec2 TexCoord;

// 11a. Create input channel through which normal vector will be received from vertex shader
// ...
in vec3 Normal;

// 26. Create input channel for vertex position passed from vertex shader
// ...

out vec4 oColor;

// 17. Add another output data for normal vector
// ...

// 27. Add another output data for position
// ...

uniform sampler2D uTexture;

void main()
{
	oColor = vec4( 0.5 );

	// 8. Sample uTexture with received texture coordinates
	// Save color read from texture to fragment shader output
	// ...
	oColor = texture(uTexture, TexCoord);

	// 13. Save normalized normal vector to color output
	// ...
	oColor.rgb = (normalize(Normal));

	// 18. Save normalized normal vector to newly created output channel
	// ...

	// 26b. Temporarily save position in color or normal output
	// ...

	// 28. Store position in newly created output channel
	// ...
}


BassPass.vp
#version 140
precision highp float;

in vec4 inPosition;

// 5. Add texture coordinates vertex attribute
// ...
in vec2 inTexCoord;

// 9. Add another vertex attribute for normal vector 
// ...
in vec3 inNormal;

// 6a. Create new output channel for texture coordinates
// ...
out vec2 TexCoord;

// 10a. Create new output channel for normal vector
// ...
out vec3 Normal;

// 25a. Create new output channel for vertex position
// ...

uniform mat4 uMVPMatrix;
uniform mat4 uModelViewMatrix;

void main()
{
	gl_Position = uMVPMatrix * inPosition;

	// 6b. Pass texture coordinates to fragment shader in a newly created output channel
	// ...
	TexCoord = inTexCoord;

	// 10b. Pass normal vector to fragment shader
	// Transform normal vector into view space with model-view matrix
	// ...
	Normal = (mat3(uModelViewMatrix))*inNormal;

	// 25b. Convert vertex position into view space using Model-View matrix
	// ...

	// 25c. Store view space vertex position in newly created channel
	// ...
}


```



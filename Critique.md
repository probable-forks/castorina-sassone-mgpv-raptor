# Criticisms

## X11 / Wayland

Neglecting to provide documentation or guidance on the compile-time configuration changes necessary for modern *Wayland*-based Linux desktops is a huge oversight – no less because the SDL 2 defaults to *Wayland* in such environments.

## Shader Compilation

I strongly dislike the way that this code-base executes `glslangValidator` for shader compilation at runtime and how environment variables are used to determine the path to that executable.

- I may be able to exploit *Naga* for both reflection and compilation from **GLSL** to **SPIR-V**.

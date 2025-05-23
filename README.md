# Advanced Fluid Dynamics Sandbox

A real-time fluid simulation sandbox built with JavaScript, featuring particle-based physics, interactive objects, and realistic water behavior.

## Features

### 🌊 Realistic Fluid Simulation
- **SPH (Smoothed Particle Hydrodynamics)** implementation for accurate fluid behavior
- **1000+ particles** running at 60fps with optimized spatial partitioning
- **Surface tension** and **viscosity** effects with real-time adjustment
- **Wave propagation** and interference patterns
- **Foam generation** from high-velocity collisions

### 🎮 Interactive Elements
- **Draggable barriers** to redirect water flow and create obstacles
- **Multiple object types**: spheres, cubes, light balls, heavy balls
- **Adjustable gravity** (including negative gravity for anti-gravity effects)
- **Real-time physics parameters** adjustment
- **Click-to-add water** particles anywhere in the simulation

### 🎨 Visual Effects
- **Metaball rendering** for smooth, realistic water appearance
- **Dynamic particle coloring** based on velocity and density
- **Realistic lighting** and highlights on objects
- **Smooth animations** with Verlet integration for stability

## Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/fluid-dynamics-sandbox.git
   cd fluid-dynamics-sandbox
   ```

2. **Run locally:**
   - Open `index.html` in your web browser
   - Or serve with a local server:
     ```bash
     python -m http.server 8000
     # Navigate to http://localhost:8000
     ```

3. **Start experimenting:**
   - Click to add water particles
   - Drag sliders to adjust physics
   - Drop objects and watch realistic interactions
   - Create barriers to redirect water flow

## Controls

### Mouse/Touch Controls
- **Click anywhere**: Add water particles
- **Drag** (in barrier mode): Create barriers to redirect water flow
- **Object buttons**: Drop different types of objects

### Keyboard Shortcuts
- **Spacebar**: Add water particles at random location
- **R**: Reset simulation
- **B**: Toggle barrier mode
- **1-4**: Drop different object types (sphere, cube, light ball, heavy ball)

### Physics Parameters
- **Gravity**: -2.0 to 3.0 (negative for anti-gravity effects)
- **Viscosity**: 0.1 to 2.0 (water thickness)
- **Surface Tension**: 0.0 to 2.0 (particle cohesion)

## Technical Implementation

### Fluid Simulation Algorithm
The simulation uses **Smoothed Particle Hydrodynamics (SPH)**, a computational method for simulating fluid flows. Key components:

1. **Spatial Partitioning**: Divides space into grid cells for efficient neighbor finding
2. **Density Calculation**: Uses smoothing kernels to calculate local density
3. **Pressure Forces**: Applies forces based on pressure gradients
4. **Viscosity Forces**: Simulates fluid resistance and internal friction
5. **Surface Tension**: Creates cohesive forces between particles

### Performance Optimizations
- **Spatial Grid**: O(n) neighbor finding instead of O(n²)
- **Verlet Integration**: Stable, efficient numerical integration
- **Adaptive Time Stepping**: Maintains stability at high speeds
- **WebGL-ready**: Optimized for GPU acceleration (can be extended)

### Physics Constants
```javascript
// Realistic water properties
const WATER_DENSITY = 1000;      // kg/m³
const REST_DENSITY = 1.0;        // Normalized
const VISCOSITY = 0.8;           // Dynamic viscosity
const SURFACE_TENSION = 0.5;     // Surface tension coefficient
const PARTICLE_MASS = 1.0;       // Normalized mass
const SMOOTHING_RADIUS = 20;     // Kernel support radius
```

## File Structure

```
fluid-dynamics-sandbox/
├── index.html              # Main simulation file
├── README.md              # This file
├── PERFORMANCE.md         # Performance optimization guide
└── examples/              # Example configurations
    ├── waterfall.html     # Waterfall simulation
    ├── dam-break.html     # Dam break scenario
    └── zero-gravity.html  # Zero gravity effects
```

## Browser Compatibility

- **Chrome/Edge**: Full support with hardware acceleration
- **Firefox**: Full support, may have slight performance differences
- **Safari**: Supported, optimized for iOS devices
- **Mobile**: Touch controls supported, performance varies by device

## Performance Tips

### For 60fps with 1000+ particles:
1. **Use Chrome or Edge** for best performance
2. **Close other browser tabs** to free up memory
3. **Reduce particle count** if experiencing lag
4. **Adjust quality settings** in the control panel
5. **Use discrete graphics** on laptops when available

### Performance Monitoring:
- **FPS Counter**: Real-time frame rate display
- **Particle Count**: Live particle count
- **Object Count**: Number of rigid bodies

## Customization

### Adding New Object Types
```javascript
// In RigidBody constructor
case 'custom':
    this.radius = 20;
    this.mass = Math.PI * this.radius * this.radius * 1.5;
    this.color = '#FF5722';
    this.restitution = 0.9; // Bounciness
    break;
```

### Modifying Fluid Properties
```javascript
// Adjust these constants in FluidParticle class
const STIFFNESS = 0.5;          // Pressure responsiveness
const DAMPING = 0.999;          // Velocity damping
const KERNEL_RADIUS = 20;       // Interaction radius
```

### Custom Rendering Effects
```javascript
// Add new visual effects in render() method
const glowGradient = this.ctx.createRadialGradient(
    particle.x, particle.y, 0,
    particle.x, particle.y, particle.radius * 3
);
glowGradient.addColorStop(0, 'rgba(0, 150, 255, 0.8)');
glowGradient.addColorStop(1, 'rgba(0, 150, 255, 0)');
```

## Contributing

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit your changes**: `git commit -m 'Add amazing feature'`
4. **Push to the branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Development Guidelines
- Maintain 60fps performance target
- Add comments for complex physics calculations
- Test on multiple browsers
- Follow existing code style
- Update documentation for new features

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- **SPH Algorithm**: Based on research by Müller et al. (2003)
- **Particle Physics**: Inspired by classical fluid dynamics
- **Rendering Techniques**: Modern web graphics optimization
- **Performance**: Optimized for real-time interactive applications

## Examples & Demos

### Basic Water Drop
```javascript
// Add water at specific location
simulation.addWater(300, 100);
```

### Create a Dam Break Scenario
```javascript
// Add barriers to create a dam
simulation.barriers.push(new Barrier(200, 300, 200, 500));
// Fill with water
for(let x = 50; x < 180; x += 10) {
    for(let y = 200; y < 400; y += 10) {
        simulation.particles.push(new FluidParticle(x, y));
    }
}
```

### Anti-Gravity Effect
```javascript
// Set negative gravity
simulation.gravity = -1.5;
// Drop objects to see them float upward
simulation.dropObject('sphere');
```

---

**Enjoy experimenting with realistic fluid dynamics!** 🌊

For questions, issues, or contributions, please visit the [GitHub repository](https://github.com/yourusername/fluid-dynamics-sandbox).

## Preguntas a responder

**1. ¿Por qué necesitamos Loki además de Prometheus si ya tenemos `/metrics`?**

Porque no se encargan de lo mismo, Prometheus te brinda el que esta pasando, ya que solo entiende numeros, pero no nos dice el motivo solo brinda la métrica. En cambio Loki almacena texto completo y dice el por qué esta pasando un evento, mostrando un log completo. Sin Loki tendriamos que estar adivinando que causó un pico en la grafica.

**2. ¿Qué ventaja aporta que las fuentes de datos de Grafana estén aprovisionadas como código y no creadas a mano?**

Permite la reproducibilidad y la automatización, ya que en caso se destruya el entorno o se lleva a produccion, el stack siempre se levanta listo para usarse, no se depende de la intervencion humana. Además de poder trabajar en un mismo entorno con un equipo de trabajo, teniendo control sobre las versiones en git, detectando errores tempranos.

**3. El panel "CPU contenedor" y el panel "CPU host" pueden mostrar valores muy distintos. ¿Por qué? ¿Cuál usarías para alertar sobre una aplicación concreta?**

Muestran valores distintos porque el CPU host representa el uso total de la maquina fisica, mientras que CPU contenedor unicamente representa el uso de ese contenedor de forma aislada, por eso es que se puede tener un valor alto en CPU contenedor y un valor bajo en CPU host. Para alertar lo mejor es CPU contenedor ya que con la del host se puede disparar la alarma por un proceso externo a la API generando un falso positivo.

**4. ¿Qué diferencia hay entre el *evaluation interval* y el *pending period* de una alarma?**

Evaluation interval representa cuanto tiempo Grafana ejecuta la consulta de Prometheus para revisar si la condicion se esta cumpliendo. Mientras que pending period representa el tiempo que la condicion debe de mantener de forma continua hasta que pase a estado Firing. Esto es vital para evitar que micro-picos de procesamiento te llenen el correo de alertas inútiles.
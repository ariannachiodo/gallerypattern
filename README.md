SUPSI 2023-24  
Corso d’interaction design, CV428.01  
Docenti: A. Gysin, G. Profeta  

Elaborato 2: Intermedio algoritmi

# Circle packing
Autore: Arianna Chiodo
 
[Circle packing demo](https://ariannachiodo.github.io/circlepacking/#headline)


## Introduzione e tema
Il “circle packing” è un affascinante problema geometrico che riguarda la disposizione di cerchi all'interno di una forma specifica nel modo più efficiente possibile. L'obiettivo principale di questo problema è massimizzare il numero di cerchi che possono essere inseriti senza sovrapposizioni all'interno di una determinata area, come un rettangolo, un cerchio più grande, o qualsiasi altra figura geometrica.




## Riferimenti progettuali
Per il mio progetto, ho preso ispirazione da tre principali riferimenti progettuali: il Responsive Design, il User-Centered Design e il Minimalist Design. Il Responsive Design, utilizzando una griglia per layout e contenuti, suggerisce un design reattivo che si adatta a vari dispositivi e dimensioni dello schermo. Il User-Centered Design, con una navigazione chiara e link a sezioni specifiche come storia, funzionamento, utilizzi, ecc., riflette un approccio focalizzato sull'utente, rendendo le informazioni facilmente accessibili. Il Minimalist Design, adottando una struttura pulita e semplice, enfatizza i contenuti piuttosto che gli ornamenti, contribuendo a un'estetica essenziale e diretta.

## Design dell’interfraccia e modalià di interazione
L'interfaccia del progetto "Circle Packing" è stata sviluppata con un design minimalista e intuitivo, focalizzato sulla visualizzazione efficace e interattiva delle informazioni. Tutte le informazioni sono organizzate in una singola pagina, permettendo agli utenti di accedere rapidamente ai contenuti desiderati tramite lo scorrimento verticale o cliccando sui pulsanti situati sulla sinistra, che li porteranno direttamente alla sezione pertinente.

Per rappresentare i concetti in modo chiaro e leggibile, ho scelto di utilizzare glifi. Questa scelta non solo migliora la comprensione e la leggibilità delle informazioni, ma contribuisce anche a rendere l'interfaccia esteticamente gradevole.

+------------------+<br>
					|&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;|<br>
					|&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;|<br>
					|&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;|<br>
					|&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;■&nbsp;&nbsp;&nbsp;&nbsp;|<br>
					+------------------+

Il layout della pagina è progettato per essere ordinato e coerente, con i glifi che aiutano a enfatizzare e illustrare i vari concetti in modo visivamente accattivante. Questo approccio garantisce un'esperienza utente piacevole e funzionale, facilitando l'interazione e l'esplorazione delle informazioni presentate.

[<img src="docs/img_01.png" width="800">]()
[<img src="docs/img_02.png" width="800">]()
[<img src="docs/img_03.png" width="800">]()


## Tecnologia usata
Il progetto "Circle Packing" utilizza CSS e HTML per gestire il layout e lo stile dell'interfaccia utente, assicurando un design minimale e intuitivo. JavaScript è impiegato per animare dinamicamente i cerchi presenti nella pagina, migliorando l'interattività e la visualizzazione dei contenuti. Questa combinazione di tecnologie permette di creare un'esperienza utente fluida e coinvolgente, ottimizzata per diversi dispositivi e dimensioni di schermo.


```		
document.querySelectorAll(".testata").forEach( el => {
	el.addEventListener('click', evt => {
		evt.target.nextElementSibling.classList.toggle("chiuso")
	})
})

var circles = [];


function setup() {
createCanvas(windowWidth, windowHeight);
// Start with a big one in the center in the hopes that it
// takes up a lot of a space and the sketch runs faster
circles.push(new Circle(width / 2, height / 2, min(width, height) / 3));
}

function draw() {
background(245);

// All the circles
for (var i = 0; i < circles.length; i++) {
var c = circles[i];
c.show();

// Is it a growing one?
if (c.growing) {
c.grow();
// Does it overlap any previous circles?
for (var j = 0; j < circles.length; j++) {
var other = circles[j];
if (other != c) {
  var d = dist(c.x, c.y, other.x, other.y);
  if (d - 1 < c.r + other.r) {
	c.growing = false;
  }
}
}

// Is it stuck to an edge?
if (c.growing) {
c.growing = !c.edges();
}
}
}

// Let's try to make a certain number of new circles each frame
// More later
var target = 1 + constrain(floor(frameCount / 120), 0, 20);
// How many
var count = 0;
// Try N times
for (var i = 0; i < 1000; i++) {
if (addCircle()) {
count++;
}
// We made enough
if (count == target) {
break;
}
}

// We can't make any more
if (count < 1) {
noLoop();
console.log("finished");
}
}

// Add one circle
function addCircle() {
// Here's a new circle
var newCircle = new Circle(random(width), random(height), 1);
// Is it in an ok spot?
for (var i = 0; i < circles.length; i++) {
var other = circles[i];
var d = dist(newCircle.x, newCircle.y, other.x, other.y);
if (d < other.r + 4) {
newCircle = undefined;
break;
}
}
// If it is, add it
if (newCircle) {
circles.push(newCircle);
return true;
} else {
return false;
}
}

// Circle object
function Circle(x, y, r) {
this.growing = true;
this.x = x;
this.y = y;
this.r = r;
}

// Check stuck to an edge
Circle.prototype.edges = function() {
return (this.r > width - this.x || this.r > this.x || this.r > height - this.y || this.r > this.y);
}

// Grow
Circle.prototype.grow = function() {
this.r += 0.5;
}

// Show
Circle.prototype.show = function() {
noFill();
strokeWeight(0.5);
stroke(0, 0, 0);
ellipse(this.x, this.y, this.r * 2);
}
```

## Target e contesto d’uso
Il progetto "Circle Packing" è versatile e si presta a diversi contesti d'uso educativi e divulgativi. Rivolgendosi principalmente agli studenti e agli appassionati di grafica e visualizzazione dati, può fungere da risorsa educativa per corsi di design, grafica o informatica. Offre una piattaforma per esplorare tecniche avanzate di visualizzazione dati e animazione, consentendo agli utenti di comprendere concetti complessi attraverso una rappresentazione visiva interattiva.

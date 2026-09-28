# portfolio_egiteko

"Proiektuko galderak erakutsi" erabilera-kasuaren inplementazioa:

1) proyectos app-ren url.py fitxategian bidea gehitu:
path("preguntas/proyecto/<int:pk>/", views.leer_preguntas, name="leer_preguntas"),

2) Gehitu leer_preguntas funtzioa views.py fitxategian. Datu-basetik proiektu batekin erlazionatutako galderak kontsultatuko ditu, eta galdera horien zerrenda JSON formatuan itzuliko du

3) proyecto_index.html txantiloian proiektu bakoitzeko esteka egokia sortu, eta horren azpian edukiontzi bat non galderak sartuko diren
                        <a class="btn btn-primary btn-galderak"
                            data-id="{{ proyecto.pk }}"
                            data-url="{% url 'leer_preguntas' proyecto.pk %}"
                            href="#">hemen</a>

<div id="galderak-{{ proyecto.pk }}"></div>


4) proyecto_index.html txantiloian gehitu Javascript egokia, galderen botoi bakoitzari listener bat lotzeko
Hemen bi modu daude egiteko:
4.1) Sinplea, baina estekak DOM-ean egon behar dira, Javascript-a egikaritzen denean
 document.querySelectorAll('.btn-galderak').forEach(function (btn) {
        btn.addEventListener('click', function (e) {
            e.preventDefault();

            const id = this.dataset.id;
            const url = this.dataset.url;
	// ...
});

4.2) Sendoa: listener bakar bat document objektuan, click gertaerak iragazten duena. Dinamikoki esteka gehiago gehituko bagenitu, funtzionatuko luke ere
document.addEventListener('click', function (e) {
    const btn = e.target.closest('.btn-galderak');
    if (!btn) return;
    e.preventDefault();

    const id = btn.dataset.id;
    const url = btn.dataset.url;
    // ... 
});
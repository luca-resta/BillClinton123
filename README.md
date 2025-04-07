### BillClinton123
<div id="poesia-comica">
  <h2>Pubblica la tua Poesia Comica!</h2>
  <textarea id="testo-poesia" placeholder="Scrivi qui la tua poesia..."></textarea><br><br>
  <button onclick="pubblicaPoesia()">Pubblica</button>

  <div id="poesie-pubblicate">
    <h3>Poesie Pubblicate</h3>
    </div>
</div>

<script>
  let poesie = [];

  function pubblicaPoesia() {
    const testoPoesia = document.getElementById("testo-poesia").value.trim();
    if (testoPoesia !== "") {
      const nuovaPoesia = {
        testo: testoPoesia,
        likes: 0
      };
      poesie.push(nuovaPoesia);
      aggiornaVisualizzazionePoesie();
      document.getElementById("testo-poesia").value = ""; // Pulisci l'area di testo
    } else {
      alert("Per favore, scrivi qualcosa prima di pubblicare!");
    }
  }

  function aggiungiLike(indicePoesia) {
    poesie[indicePoesia].likes++;
    aggiornaVisualizzazionePoesie();
  }

  function aggiornaVisualizzazionePoesie() {
    const contenitorePoesie = document.getElementById("poesie-pubblicate");
    contenitorePoesie.innerHTML = "<h3>Poesie Pubblicate</h3>"; // Rimuovi le poesie precedenti

    poesie.forEach((poesia, indice) => {
      const divPoesia = document.createElement("div");
      divPoesia.classList.add("poesia");
      divPoesia.innerHTML = `
        <p>${poesia.testo}</p>
        <button onclick="aggiungiLike(${indice})">Mi Piace: <span id="likes-${indice}">${poesia.likes}</span></button>
        <hr>
      `;
      contenitorePoesie.appendChild(divPoesia);
    });
  }

  // Stile CSS di base (puoi personalizzarlo ulteriormente)
  const style = document.createElement('style');
  style.textContent = `
    #poesia-comica {
      font-family: sans-serif;
      margin-top: 20px;
      padding: 15px;
      border: 1px solid #ccc;
      border-radius: 5px;
      background-color: #f9f9f9;
    }

    #testo-poesia {
      width: 100%;
      min-height: 100px;
      margin-bottom: 10px;
      padding: 8px;
      box-sizing: border-box;
      border: 1px solid #ddd;
      border-radius: 3px;
    }

    button {
      padding: 8px 15px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 3px;
      cursor: pointer;
    }

    button:hover {
      background-color: #0056b3;
    }

    #poesie-pubblicate {
      margin-top: 20px;
    }

    .poesia {
      margin-bottom: 15px;
      padding: 10px;
      border: 1px solid #eee;
      border-radius: 3px;
      background-color: white;
    }

    .poesia p {
      margin-top: 0;
    }
  `;
  document.head.appendChild(style);
</script>

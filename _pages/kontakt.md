---
title: "Kontakt"
---
<form id="my-form" action="https://formspree.io/f/xdorqojo" method="POST" style= "background-color : #589436;   border-radius: 25px;" >
  <label style="color: black ">Vorname:</label>
  <input type="text" name="vorname" required />
  <label>Nachname:</label>
  <input type="text" name="nachname" required />
  <label>E-Mail-Adresse:</label>
  <input type="email" name="email" required />
  <label>Betreff:</label>
  <input type="text" name="betreff" required />
  <label>Nachricht:</label>
  <textarea name="nachricht" cols="40" rows="5" required></textarea>
<!-- TODO Datenschutz -->
  <button id="my-form-button" style="float: right;">Senden</button>
  <p style="color: black;">Durch die Nutzung des Kontaktformulars werden die <a href="/_pages/datenschutz"> Datenschutzbestimmungen </a> akzeptiert.</p> 
  <p id="my-form-status" style="color: black;"></p> 
</form>
<!-- Place this script at the end of the body tag -->
<script>
    var form = document.getElementById("my-form");
    
    async function handleSubmit(event) {
      event.preventDefault();
      var status = document.getElementById("my-form-status");
      var data = new FormData(event.target);
      fetch(event.target.action, {
        method: form.method,
        body: data,
        headers: {
            'Accept': 'application/json'
        }
      }).then(response => {
        if (response.ok) {
          status.innerHTML = "Die Nachricht wurde erfolgreich versendet!";
          form.reset()
        } else {
          response.json().then(data => {
            if (Object.hasOwn(data, 'errors')) {
              status.innerHTML = data["errors"].map(error => error["message"]).join(", ")
            } else {
              status.innerHTML = "Oops! There was a problem submitting your form"
            }
          })
        }
      }).catch(error => {
        status.innerHTML = "Oops! There was a problem submitting your form"
      });
    }
    form.addEventListener("submit", handleSubmit)
</script>

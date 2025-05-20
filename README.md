<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Le Gentleman - Réservation Barber Shop</title>
  <style>
    /* Reset & base */
    * {
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    body {
      margin: 0; padding: 0; background: #f9f8f6; color: #222;
      display: flex; flex-direction: column; align-items: center; min-height: 100vh;
      padding: 20px;
    }

    header {
      width: 100%; max-width: 480px; 
      background: #1c1c1c; color: #f3f3f3; 
      padding: 20px;
      text-align: center;
      border-radius: 8px 8px 0 0;
      box-shadow: 0 2px 8px rgb(0 0 0 / 0.3);
      margin-bottom: 20px;
    }
    header h1 {
      margin: 0;
      font-weight: 900;
      letter-spacing: 1.1em;
      font-size: 2.2rem;
      font-family: 'Georgia', serif;
      user-select: none;
    }
    header small {
      display: block;
      font-weight: 400;
      letter-spacing: 0.05em;
      font-size: 0.85rem;
      color: #ccc;
      margin-top: 4px;
    }

    main {
      background: #fff; 
      max-width: 480px; 
      width: 100%;
      border-radius: 0 0 8px 8px;
      padding: 20px 25px 40px 25px;
      box-shadow: 0 3px 15px rgb(0 0 0 / 0.1);
    }

    h2 {
      margin-top: 0;
      color: #111;
      border-bottom: 2px solid #333;
      padding-bottom: 4px;
    }

    /* Liste des services */
    ul#services {
      list-style: none;
      padding-left: 0;
      margin: 10px 0 30px 0;
    }
    ul#services li {
      background: #f0ece7;
      margin-bottom: 8px;
      padding: 12px 14px;
      border-radius: 6px;
      box-shadow: inset 0 1px 3px rgb(255 255 255 / 0.7);
      font-weight: 600;
      color: #3a3a3a;
      user-select: none;
    }

    /* Form */
    form {
      display: flex; flex-direction: column;
    }
    label {
      margin-bottom: 4px;
      font-weight: 600;
      color: #444;
    }
    input, select, button {
      margin-bottom: 15px;
      padding: 10px 12px;
      font-size: 1rem;
      border: 2px solid #bbb;
      border-radius: 6px;
      transition: border-color 0.3s ease;
    }
    input:focus, select:focus {
      outline: none;
      border-color: #1c1c1c;
      box-shadow: 0 0 4px #1c1c1caa;
    }

    button#payBtn {
      background: #1c1c1c;
      color: #f9f9f9;
      font-weight: 700;
      border: none;
      cursor: pointer;
      user-select: none;
      transition: background-color 0.3s ease;
    }
    button#payBtn:hover:not(:disabled) {
      background: #444;
    }
    button:disabled {
      opacity: 0.5;
      cursor: default;
    }

    /* Confirmation */
    #confirmation {
      background: #dff0d8;
      border: 2px solid #a3c293;
      color: #3c763d;
      padding: 15px 18px;
      border-radius: 8px;
      margin-top: 20px;
      display: none;
      user-select: text;
    }

    /* Admin (liste RDV) */
    #admin {
      margin-top: 40px;
      border-top: 2px solid #ccc;
      padding-top: 20px;
    }
    #admin h3 {
      margin-bottom: 10px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.9rem;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 8px 12px;
      text-align: left;
    }
    th {
      background-color: #1c1c1c;
      color: white;
    }
    tbody tr:nth-child(even) {
      background: #f9f9f9;
    }
  </style>
</head>
<body>
  <header>
    <h1>Le Gentleman</h1>
    <small>Barber Shop - Réservation en ligne</small>
  </header>

  <main>
    <section id="services-section">
      <h2>Nos Services</h2>
      <ul id="services">
        <li>Coupe classique - 3000 FCFA</li>
        <li>Coupe dégradé - 4000 FCFA</li>
        <li>Taille de barbe - 1500 FCFA</li>
        <li>Rasage à l'ancienne - 2500 FCFA</li>
        <li>Coloration - 6000 FCFA</li>
        <li>Massage du cuir chevelu - 3500 FCFA</li>
      </ul>
    </section>

    <section id="reservation-section">
      <h2>Réserver un Rendez-vous</h2>
      <form id="reservationForm" autocomplete="off">
        <label for="clientName">Nom complet</label>
        <input type="text" id="clientName" name="clientName" required placeholder="Ex: Abdoulaye Ndiaye" />

        <label for="serviceSelect">Service</label>
        <select id="serviceSelect" name="serviceSelect" required>
          <option value="" disabled selected>-- Choisissez un service --</option>
          <option value="Coupe classique">Coupe classique - 3000 FCFA</option>
          <option value="Coupe dégradé">Coupe dégradé - 4000 FCFA</option>
          <option value="Taille de barbe">Taille de barbe - 1500 FCFA</option>
          <option value="Rasage à l'ancienne">Rasage à l'ancienne - 2500 FCFA</option>
          <option value="Coloration">Coloration - 6000 FCFA</option>
          <option value="Massage du cuir chevelu">Massage du cuir chevelu - 3500 FCFA</option>
        </select>

        <label for="date">Date</label>
        <input type="date" id="date" name="date" required min="" />

        <label for="time">Heure</label>
        <input type="time" id="time" name="time" required min="10:00" max="21:00" />

        <button type="submit" id="payBtn">Payer maintenant</button>
      </form>

      <div id="confirmation"></div>
    </section>

    <section id="admin">
      <h3>Espace Admin - Rendez-vous réservés</h3>
      <table>
        <thead>
          <tr>
            <th>Nom</th>
            <th>Service</th>
            <th>Date</th>
            <th>Heure</th>
          </tr>
        </thead>
        <tbody id="appointmentsList">
          <tr><td colspan="4" style="text-align:center; color:#999;">Aucun rendez-vous pour l'instant</td></tr>
        </tbody>
      </table>
    </section>
  </main>

  <script>
    // Initialisation date min = aujourd'hui
    const dateInput = document.getElementById('date');
    const today = new Date().toISOString().split('T')[0];
    dateInput.min = today;

    // Gérer la liste des rendez-vous en session
    let appointments = [];

    // Mise à jour tableau admin
    function updateAppointmentsTable() {
      const tbody = document.getElementById('appointmentsList');
      if (appointments.length === 0) {
        tbody.innerHTML = '<tr><td colspan="4" style="text-align:center; color:#999;">Aucun rendez-vous pour l\'instant</td></tr>';
        return;
      }
      tbody.innerHTML = '';
      appointments.forEach(({name, service, date, time}, idx) => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${name}</td>
          <td>${service}</td>
          <td>${date}</td>
          <td>${time}</td>
        `;
        tbody.appendChild(tr);
      });
    }

    // Form submit handler
    document.getElementById('reservationForm').addEventListener('submit', function(e) {
      e.preventDefault();

      const name = this.clientName.value.trim();
      const service = this.serviceSelect.value;
      const date = this.date.value;
      const time = this.time.value;

      // Validation horaire (10h - 21h)
      const [hour, minute] = time.split(':').map(Number);
      if (hour < 10 || hour > 21 || (hour === 21 && minute > 0)) {
        alert("Veuillez choisir une heure entre 10h00 et 21h00.");
        return;
      }

      // Simuler paiement fictif
      const payBtn = document.getElementById('payBtn');
      payBtn.disabled = true;
      payBtn.textContent = "Paiement en cours...";

      setTimeout(() => {
        // Ajout du rendez-vous dans la liste
        appointments.push({name, service, date, time});
        updateAppointmentsTable();

        // Afficher confirmation
        const conf = document.getElementById('confirmation');
        conf.style.display = 'block';
        conf.innerHTML = `
          <strong>Réservation confirmée !</strong><br>
          Merci <em>${name}</em>.<br>
          Service : <strong>${service}</strong><br>
          Date : <strong>${date}</strong><br>
          Heure : <strong>${time}</strong><br>
          Nous avons hâte de vous accueillir au Barber Shop Le Gentleman.
        `;

        // Reset form
        this.reset();
        dateInput.min = today;

        payBtn.disabled = false;
        payBtn.textContent = "Payer maintenant";
      }, 1500); // simulation paiement 1.5s
    });
  </script>
</body>
</html>

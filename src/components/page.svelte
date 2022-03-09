<script lang="ts">
  import "animate.css";
  let amount: number;
  let brutusTaxes: number = 0;
  let liquidTaxes: number = 0;
  let valBrutus: number = 0;
  let valLiquid: number = 0;
  let brutus: number = 0;
  let valBrutusRounded: number = 0;

  //función para convertir valores
  const getValues = (value: number) => {
    valBrutus = value / 0.8775;
    valBrutusRounded = Math.round((valBrutus + Number.EPSILON) * 100) / 100;
    valLiquid = value;
    liquidTaxes = valBrutus - value;
    brutusTaxes = value * 0.1225;
    brutus = value - brutusTaxes;
  };

  //función para convertir valor en moneda
  let convertirMoneda = (monto) => {
    const dollars = new Intl.NumberFormat(`es-CH`, {
      currency: `CLP`,
      style: "currency",
    }).format(monto);

    if (monto == "") {
      return "0.00";
    } else {
      return dollars;
    }
  };

  function copyToClickBoard(copy) {
    let total;
    total = copy.toString().replace(/\./g, ",");
    if (copy > 0) {
      navigator.clipboard
        .writeText(total)
        .then(() => {
          alert(
            "El monto ha sido copiado $" +
              total +
              " será redireccionado al SII. Para realizar Boleta simplemente presione click derecho y pegue el valor en la celda 'Valor 1'"
          );
          window.open("https://www.sii.cl/servicios_online/1040-1287.html");
        })
        .catch((err) => {
          console.log("Algo salió mal", err);
        });
    } else {
      alert("el valor debe ser mayor a 0");
    }
  }
</script>

<div class="page-container">
  <div class="animate__animated animate__bounce col-12 mb-3">
    <h5>Ingresa el Monto:</h5>
    <div class="container-input">
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <span class="input-dollar" id="basic-addon1">$</span>
        </div>
        <input
          type="number"
          class="form-control"
          placeholder="150.000"
          aria-label="Username"
          aria-describedby="basic-addon1"
          bind:value={amount}
          on:input={() => getValues(amount)}
        />
      </div>
    </div>

    <hr />
  </div>
  <div class="container animate__animated animate__slideInUp">
    <div class="row">
      <div class="col-12 col-md-6">
        <div class="card rounded-5">
          <h5 class="card-header1">Valor Líquido</h5>
          <div class="card-body">
            <h5 class="card-title">¿Cómo Funciona?</h5>
            <p class="card-amount">
              El Emisor de la boleta recibe el 100% del valor de la misma.
            </p>
            <hr />
            <p class="card-text">
              Realizar Boleta por: <span class="card-amount"
                >$ {convertirMoneda(valBrutus)}</span
              >
            </p>
            <p class="card-text">
              Retención Sii: <span class="card-amount"
                >$ {convertirMoneda(liquidTaxes)}</span
              >
            </p>
            <p class="card-text">
              Recibes Líquido: <span class="card-amount"
                >$ {convertirMoneda(valLiquid)}</span
              >
            </p>
            <a
              on:click={() => copyToClickBoard(valBrutusRounded)}
              href="#"
              class="btn btn-primary">Copiar valor e ir al SII</a
            >
          </div>
        </div>
      </div>
      <div class="col-12 col-md-6">
        <div class="card rounded-5">
          <h5 class="card-header2">Valor Bruto</h5>
          <div class="card-body">
            <h5 class="card-title">¿Cómo funciona?</h5>
            <p class="card-amount">
              El Emisor de la boleta debe pagar el impuesto, por lo que recibe
              menos.
            </p>
            <hr />
            <p class="card-text">
              Realizar boleta por: <span class="card-amount"
                >$ {convertirMoneda(valLiquid)}</span
              >
            </p>
            <p class="card-text">
              Retención SII: <span class="card-amount"
                >$ {convertirMoneda(brutusTaxes)}</span
              >
            </p>
            <p class="card-text">
              Recibes Líquido: <span class="card-amount"
                >$ {convertirMoneda(brutus)}</span
              >
            </p>
            <a
              on:click={() => copyToClickBoard(valLiquid)}
              href="#"
              class="btn btn-primary">Copiar valor e ir al SII</a
            >
          </div>
        </div>
      </div>
    </div>
  </div>
  <hr />
  <h6>Diseñado por Alejandro Rodríguez</h6>
  <h7>@im_alejandrorodriguez</h7>
</div>

<style>
  .page-container {
    width: fit-content;
    margin-top: 2rem;
    margin-right: auto;
    margin-left: auto;
    margin-bottom: 5rem;
    padding: 2rem;
    text-align: center;
    background-color: rgb(255, 255, 255);
    border-radius: 0.5rem;
    box-shadow: 10px 10px;
  }

  .card-header1 {
    background-color: rgb(222, 11, 80);
    color: aliceblue;
    padding: 0.8rem;
    font-size: 20px;
    border-top-right-radius: 1rem;
    border-top-left-radius: 1rem;
  }

  .card-header2 {
    background-color: rgb(200, 254, 96);
    padding: 0.8rem;
    font-size: 20px;
    border-top-right-radius: 1rem;
    border-top-left-radius: 1rem;
  }

  .card {
    margin-top: 1rem;
    border-radius: 1rem;
    box-shadow: 0 4px 5px 0 rgba(0, 0, 0, 0.2),
      0 12px 30px 0 rgba(0, 0, 0, 0.19);
    min-height: 370px;
  }

  .card:hover {
    background-color: rgb(230, 230, 230);
    box-shadow: 0 10px 20px 0 rgba(72, 10, 216, 0.2),
      0 30px 30px 0 rgba(0, 0, 0, 0.19);
  }

  .card-text {
    font-weight: bold;
  }

  .card-amount {
    font-weight: normal;
  }

  .container-input {
    max-width: 260px;
    display: inline-block;
  }

  .input-dollar {
    display: flex;
    align-items: center;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #ffffff;
    text-align: center;
    white-space: nowrap;
    background-color: rgb(9, 70, 128);
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
  }

  .input-dollar:hover {
    background-color: rgb(160, 7, 78);
    border-color: rgb(160, 7, 78);
  }

  .btn-primary {
    background-color: rgb(9, 70, 128);
    border-color: rgb(9, 70, 128);
  }

  .btn-primary:hover {
    background-color: rgb(160, 7, 78);
    border-color: rgb(160, 7, 78);
  }
</style>

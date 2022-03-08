<script lang="ts">
  let amount: number;
  let brutusTaxes: number = 0;
  let liquidTaxes: number = 0;
  let valBrutus: number = 0;
  let valLiquid: number = 0;
  let brutus: number = 0;

  //función para convertir valores
  const getValues = (value: number) => {
    valBrutus = value / 0.8775;
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
          type="text"
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
  <div class="container">
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
              href="https://www.sii.cl/servicios_online/3532-.html"
              class="btn btn-primary">Ir al SII</a
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
              El Emisor de la boleta recibe el 100% del valor de la misma.
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
              href="https://www.sii.cl/servicios_online/3532-.html"
              class="btn btn-primary">Ir al SII</a
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

  .btn-primary {
    background-color: rgb(9, 70, 128);
    border-color: rgb(9, 70, 128);
  }
</style>

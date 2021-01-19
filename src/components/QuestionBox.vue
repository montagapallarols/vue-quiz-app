<template>
  <div>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <b-jumbotron>
            <template #lead>
              Here goes the question?
            </template>

            <hr class="my-4" />

            <p>
              List of answers
            </p>

            <b-button variant="primary" href="#">Submit</b-button>
            <b-button variant="success" href="#">Next</b-button>
          </b-jumbotron>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

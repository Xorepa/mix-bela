<template>
  <q-page padding>
    <h1>Contatos</h1>
    <div class="q-pa-md">
      <div class="q-gutter-y-md">
        <q-card>
          <q-card-section>
            <div class="text-h6">Nossos Contatos</div>
            <div class="q-mt-md">
              <p><q-icon name="phone" /> (11) 1234-5678</p>
              <p><q-icon name="email" /> contato@mixbela.com.br</p>
              <p><q-icon name="location_on" /> Rua Exemplo, 123 - São Paulo/SP</p>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
defineOptions({
  name: 'ContatosPage'
});
</script>

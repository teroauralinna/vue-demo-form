<template>
  <div>
    <form v-if="!isSubmitted" @submit.prevent="submit" novalidate>
      <div class="form-group">
        <label for="firstName">{{ $t('form.firstName') }} *</label>
        <input type="text" class="form-control" id="firstName" v-model.lazy.trim="form.firstName" @blur="onFieldBlur('firstName')" v-bind:class="getFieldClasses('firstName')">
        <div v-if="isErrorField('firstName')" class="invalid-feedback">{{ $t('error.fieldRequired', { field: $t('form.firstName') }) }}</div>
      </div>
      <div class="form-group">
        <label for="lastName">{{ $t('form.lastName') }} *</label>
        <input type="text" class="form-control" id="lastName" v-model.lazy.trim="form.lastName" @blur="onFieldBlur('lastName')" v-bind:class="getFieldClasses('lastName')">
        <div v-if="isErrorField('lastName')" class="invalid-feedback">{{ $t('error.fieldRequired', { field: $t('form.lastName') }) }}</div>
      </div>
      <div class="form-group">
        <label for="email">{{ $t('form.email') }} *</label>
        <input type="email" class="form-control" id="email" v-model.lazy.trim="form.email" @blur="onFieldBlur('email')" v-bind:class="getFieldClasses('email')">
        <div v-if="isErrorField('email')" class="invalid-feedback">{{ $t('error.fieldInvalid', { field: $t('form.email') }) }}</div>
      </div>
      <div class="form-group">
        <label for="type">{{ $t('form.type') }} *</label>
        <select id="type" class="form-control" v-model="form.type" @blur="onFieldBlur('type')" v-bind:class="getFieldClasses('type')">
            <option v-for="type in types" v-bind:key="type.value" v-bind:value="type.value">{{ $t(type.label) }}</option>
        </select>
        <div v-if="isErrorField('type')" class="invalid-feedback">{{ $t('form.type') }}</div>
      </div>
      <div class="form-group">
        <label for="additionalInfo">{{ $t('form.additionalInfo') }}</label>
        <textarea 
          type="additionalInfo" 
          class="form-control" 
          id="additionalInfo" 
          v-model.trim="form.additionalInfo" 
          v-bind:class="getFieldClasses('additionalInfo')" 
          v-bind:maxlength="$v.form['additionalInfo'].$params.maxLength.max" 
          @blur="onFieldBlur('additionalInfo')">
        </textarea>
        <small class="text-muted form-text">{{ $tc('form.charactersLeft', getCharactersLeft('additionalInfo'), { charCount: getCharactersLeft('additionalInfo') }) }}</small>
        <div v-if="isErrorField('additionalInfo')" class="invalid-feedback">{{ $t('error.fieldMaxLength', { field: $t('form.additionalInfo') }) }}</div>
      </div>
      <div class="form-group">
        <div class="form-check">
          <input type="checkbox" class="form-check-input" id="terms" v-model.lazy.trim="form.terms" @change="onFieldBlur('terms')" v-bind:class="getFieldClasses('terms')">
          <label class="form-check-label" for="terms">{{ $t('form.terms') }} *</label>
        </div>
      </div>
      <div class="alert alert-danger" v-if="isError">
        <p class="mb-0">
          <strong>{{ $t(errorHeader) }}</strong>
        </p>
        <ul class="mb-0 pl-3" v-if="errors.length > 0">
          <li v-for="error in errors" v-bind:key="error.field">
            <span v-if="error.field">{{ $t('form.'+error.field) }}<span v-if="error.message">: {{ $t(error.message) }}</span></span>
            <span v-else-if="error.message">{{ $t(error.message) }}</span>
          </li>
        </ul>
      </div>
      <div class="form-group">
        <button type="submit" class="btn btn-primary" :disabled="submitting">
          <span v-if="submitting">{{ $t('form.submitting' ) }} <img src="../../assets/loader.svg" /></span>
          <span v-else>{{ $t('form.submit' ) }}</span>
        </button>
      </div>
    </form>
    <div v-else>
      <div class="alert alert-success">
        <strong>{{ $t('form.submitted' ) }}</strong>
      </div>
      <div class="alert alert-info">
        <p><strong>{{ $t('form.sentInfo' ) }}</strong></p>
        <pre>
            {{form}}
        </pre>
      </div>
      <p class="text-center">
        <a href="#" class="btn btn-secondary" @click.prevent="reload()">{{ $t('form.return' ) }}</a>
      </p>
    </div>
  </div>
</template>

<script src="./Form.js"></script>
<style src="./Form.scss" lang="scss" scoped></style>

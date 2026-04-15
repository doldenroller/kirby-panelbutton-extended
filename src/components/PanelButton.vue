<template>
  <k-field :name="name" :label="label" :help="help">
    <k-button
      :style="{ width: fullwidth && '100%' }"
      variant="filled"
      :theme="hasError ? 'negative' : theme"
      :size="size"
      :icon="!hasError && !isLoading && icon"
      :disabled="hasError || isLoading || disabled"
      @click="onClick"
      >{{ hasError ? "Error" : isLoading ? "Please wait…" : text }}</k-button
    >
  </k-field>
</template>

<script>
export default {
  props: {
    name: String,
    label: String,
    text: String,
    url: String,
    theme: String,
    fullwidth: Boolean,
    size: String,
    icon: String,
    help: String,
    disabled: Boolean,
    open: Boolean,
    reload: Boolean,
    dialog: Boolean,
    dialogtext: String,
    redirect: String,
    isLoading: true,
    hasError: false,
  },
  methods: {
    onClick() {

      // create hook function
      function callWebHook(hook){
        // call webhook
        hook.isLoading = true;
        fetch(hook.url)
          .then((resp) => {
            if (!resp.ok) throw resp;

            if(hook.redirect){
              let path = window.panel.url('pages/' + hook.redirect);
              hook.$go(path)
            } else {
              return hook.reload && hook.$reload();
            }
          })
          .catch(() => {
            hook.hasError = true;
          })
          .then(() => {
            hook.isLoading = false;
          });
      }


      if (this.open === true) {
        // open url in new window
        window.open(this.url, "_blank");
      } else if (this.dialog === true) {
        this.$panel.dialog.open({
          component: 'k-text-dialog',
          props: {
            text: this.dialogtext ?? 'Call Hook',
          },
          on: {
            submit: () => {
              callWebHook(this);
            }
          },

        })
      } else {
        callWebHook(this);
      }

    }, // end onClick
  },
};
</script>

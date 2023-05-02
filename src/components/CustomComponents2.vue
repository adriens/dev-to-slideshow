<template>
    <div class="organization-info">
        <h1>{{ organization.name }}</h1>
        <p>Nom d'utilisateur : {{ organization.username }}</p>
        <p>URL du site web : <a :href="organization.url" target="_blank">{{ organization.url }}</a></p>
        <img :src="organization.profile_image" alt="Image de profil" />
    </div>
</template>
  
<script>
export default {
    name: 'OrganizationInfo',
    data() {
        return {
            organization: {}
        };
    },
    async created() {
        try {
            const apiUrl = 'https://dev.to/api/organizations/optnc';
            const response = await fetch(apiUrl);
            const data = await response.json();

            if (response.ok) {
                this.organization = data;
            } else {
                console.error('Erreur lors de la récupération des données de l\'organisation :', data.error);
            }
        } catch (error) {
            console.error('Erreur lors de la récupération des données de l\'organisation :', error);
        }
    }
};
</script>
  
<style scoped>
.organization-info {
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 600px;
    margin: 0 auto;
    color: black;
}

img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    object-fit: cover;
}

h1 {
    font-weight: bold;
}
</style>
  
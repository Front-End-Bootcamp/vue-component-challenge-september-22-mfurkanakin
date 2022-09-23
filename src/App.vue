<script setup>
import { objectToString } from "@vue/shared";
import {onMounted} from "vue";

async function fetchData() {
	const allData = await fetch('https://raw.githubusercontent.com/Front-End-Bootcamp/vue-bootcamp/d6f881aec77f15a4107eafc10f6a91e90f9268a4/homework%201/data.json')
		.then(data => data.json())
		.then(response => response);
		return allData

}
function getGroupNames(data) {
		const groupNames = data.map(person => person.group);
		const uniqueNames = [...new Set(groupNames)]
		console.log('groupNames', uniqueNames)
		return uniqueNames;
}
function filterByGroups(data){
	const groups = data.reduce((currentData,person) => {
		currentData[person.group] = []
		return currentData;
	},{});

	Object.keys(groups).forEach(group => {
		const students = data.filter(person => person.group == group);
		groups[group] = students;
	})
	return groups;
}



// const DATA = fetchData();
// getGroupNames(DATA);
//birbirini beklemedi await neden bekletmedi yukarda data.map not defined hatası verdi?

fetchData().then((response)=>(
	filterByGroups(response)
));


</script>

<template>
	<div>

	</div>
</template>

<style scoped>
</style>

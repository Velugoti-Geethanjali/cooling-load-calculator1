document.addEventListener("DOMContentLoaded", function() {
    const form = document.getElementById("cooling-load-form");
    const resultDiv = document.getElementById("result");

    form.addEventListener("submit", function(event) {
        event.preventDefault();

        const area = parseFloat(form.elements["area"].value);
        const occupants = parseInt(form.elements["occupants"].value);
        const buildingType = form.elements["building-type"].value;
        const outdoorTemp = parseFloat(form.elements["outdoor-temp"].value);
        const indoorTemp = parseFloat(form.elements["indoor-temp"].value);

        const coolingLoad = (buildingType === "residential") ? 100 * occupants : 150 * occupants;
        const U = 30;
        const qConduction = U * area * (outdoorTemp - indoorTemp);
        const sensibleCoolingLoad = qConduction + coolingLoad;

        resultDiv.innerHTML = `Sensible Cooling Load: ${sensibleCoolingLoad.toFixed(2)} W`;
    });
});

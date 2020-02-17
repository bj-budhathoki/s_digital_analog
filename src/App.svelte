<script>
  import { onMount } from "svelte";
  let response;
  let hourDeg;
  let minuteDeg;
  let secondDeg;
  let degitalTime;

  onMount(async () => {
    let res = await fetch(
      "http://10.10.99.200:8080/client/app/get-data/?appdata_id=0712e6fd-1d99-4962-9701-c0d90797f863"
    );
    let data = await res.json();
    dateFormat = data.appData.dateFormat;
    response = data.appData;
    response = data;
    setDate();
  });
  function setDate() {
    if (response) {
      let currentDate = new Date()
        .toLocaleString(response.data.code, {
          timeZone: response.timeZone,
          hour12: response.timeFormat === "12 Hours" ? true : false
        })
        .split(" ");

      let currentTime = currentDate[1].split(":");
      console.log("current time ::", currentTime);
      hourDeg = (currentTime[0] / 12) * 360;
      minuteDeg = (currentTime[1] / 60) * 360;
      secondDeg = (currentTime[2] / 60) * 360 + 360;
      // todayDate = currentDate[0];
      // ampm = currentDate[2];
      degitalTime =
        `0${currentTime[0]}`.slice(-2) +
        ":" +
        `0${currentTime[1]}`.slice(-2) +
        ":" +
        `0${currentTime[2]}`.slice(-2);
    }

    // const now = new Date();
    // //seconds
    // const second = now.getSeconds();
    // secondDeg = (second / 60) * 360 + 360;
    // //minutes
    // const minute = now.getMinutes();
    // minuteDeg = (minute / 60) * 360;
    // //hours
    // const hour = now.getHours();
    // hourDeg = (hour / 12) * 360;
    // degitalTime =
    //   `0${hour}`.slice(-2) +
    //   ":" +
    //   `0${minute}`.slice(-2) +
    //   ":" +
    //   `0${second}`.slice(-2);
  }
  setInterval(setDate, 1000);
</script>

<style>
  .wrapper {
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .wrapper::after {
    content: "";
  }
  .clock {
    width: 300px;
    height: 300px;
    border-radius: 50%;
    background-color: antiquewhite;
    margin: 100px auto 0px auto;
    position: relative;
    border: 20px solid cornsilk;
  }
  .center {
    background-color: #000;
    position: absolute;
    left: calc(50% - 10px);
    top: calc(50% - 10px);
    width: 20px;
    height: 20px;
    border-radius: 50%;
    z-index: 20;
  }
  .hourHand {
    width: 10px;
    height: 75px;
    background-color: #000;
    transform-origin: bottom center;
    border-radius: 4px;
    position: absolute;
    top: 75px;
    left: 145px;
    z-index: 10;
    transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
    transform: rotate(360deg);
  }
  .minuteHand {
    width: 5px;
    height: 120px;
    background-color: #000;
    transform-origin: bottom center;
    border-radius: 4px;
    position: absolute;
    top: 30px;
    left: 147px;
    z-index: 9;
    transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
    transform: rotate(90deg);
  }
  .secondHand {
    width: 2px;
    height: 120px;
    background-color: red;
    transform-origin: bottom center;
    border-radius: 4px;
    position: absolute;
    top: 30px;
    left: 149px;
    transition: all 0.06s;
    transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
    z-index: 8;
    transform: rotate(360deg);
  }
  .time {
    position: absolute;
    top: 45%;
    left: 10%;
    border: 1px solid #fff8dc;
    background-color: #fff;
    padding: 0 5px 5px 5px;
    display: block;
    box-shadow: inset 0px 2px 5px rgba(0, 0, 0, 0.4);
    border-radius: 5px;
    min-width: 70px;
    height: 15px;
  }
  .time small {
    color: red;
    transition: all 0.05s;
    transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
  }

  .clock ul {
    list-style: none;
    padding: 0;
  }
  .clock ul li {
    position: absolute;
    width: 20px;
    height: 20px;
    text-align: center;
    line-height: 20px;
    font-size: 10px;
    color: red;
  }
  .clock ul li:nth-child(1) {
    right: 22%;
    top: 6.5%;
  }
  .clock ul li:nth-child(2) {
    right: 6%;
    top: 25%;
  }
  .clock ul li:nth-child(3) {
    right: 1%;
    top: calc(50% - 10px);
    color: #000;
    font-size: 20px;
    font-weight: bold;
  }
  .clock ul li:nth-child(4) {
    right: 6%;
    top: 69%;
  }
  .clock ul li:nth-child(5) {
    right: 22%;
    top: 84%;
  }
  .clock ul li:nth-child(6) {
    right: calc(50% - 10px);
    top: calc(99% - 20px);
    color: #000;
    font-size: 20px;
    font-weight: bold;
  }
  .clock ul li:nth-child(7) {
    left: 22%;
    top: 84%;
  }
  .clock ul li:nth-child(8) {
    left: 6%;
    top: 69%;
  }
  .clock ul li:nth-child(9) {
    left: 1%;
    top: calc(50% - 10px);
    color: #000;
    font-size: 20px;
    font-weight: bold;
  }
  .clock ul li:nth-child(10) {
    left: 6%;
    top: 25%;
  }
  .clock ul li:nth-child(11) {
    left: 22%;
    top: 6.5%;
  }
  .clock ul li:nth-child(12) {
    right: calc(50% - 10px);
    top: 1%;
    color: #000;
    font-size: 20px;
    font-weight: bold;
  }
</style>

<div
  class="wrapper"
  style="background-image:url('https://cdn.pixabay.com/photo/2012/08/27/14/19/evening-55067_960_720.png')">
  <div class="clock">
    <div class="hourHand" style={`transform:rotate(${hourDeg}deg);`} />
    <div class="minuteHand" style={`transform:rotate(${minuteDeg}deg);`} />
    <div class="secondHand" style={`transform:rotate(${secondDeg}deg);`} />
    <div class="center" />
    <div class="time">
      <span>{degitalTime}</span>
    </div>
    <ul>
      <li>
        <span>1</span>
      </li>
      <li>
        <span>2</span>
      </li>
      <li>
        <span>3</span>
      </li>
      <li>
        <span>4</span>
      </li>
      <li>
        <span>5</span>
      </li>
      <li>
        <span>6</span>
      </li>
      <li>
        <span>7</span>
      </li>
      <li>
        <span>8</span>
      </li>
      <li>
        <span>9</span>
      </li>
      <li>
        <span>10</span>
      </li>
      <li>
        <span>11</span>
      </li>
      <li>
        <span>12</span>
      </li>
    </ul>
  </div>

</div>

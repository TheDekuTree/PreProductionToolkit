<template>
  <div class="home">
    <div class="n-header-bg">
      <h1 class="mainTitle">Dashboard</h1>
      <h1 class="subTitle"></h1>
    </div>
    <div style class="offsetMain ui four column doubling stackable">
      <div class="ui raised very padded text container segment">
        <h1 class="ui">Generate Schedules</h1>

        <div class="ui labeled input">
          <div class="ui label">Total Shots</div>
          <input type="text" placeholder="100" v-model="totalShots">
        </div>
        <br>
        <br>
        <div class="ui toggle checkbox">
          <input type="checkbox" name="public">
          <label>Include space for shot lengths?</label>
        </div>
        <br>
        <br>
        <div class="ui toggle checkbox">
          <input type="checkbox" name="public">
          <label>Include space for shooting dates?</label>
        </div>

        <h2>Props</h2>

        <div class="ui right labeled left icon input">
          <i class="briefcase icon"></i>
          <input
            type="text"
            placeholder="Enter Props"
            id="PropTags"
            v-model="propInput"
            v-on:keyup.enter="addProp(propInput)"
          >
          <a class="ui tag label" v-on:click="addProp(propInput)">Add Prop</a>
        </div>

        <div class="ui grid n-padding">
          <div v-for="prop in props">
            <button
              class="ui labeled icon button mini"
              style="margin-top: 12px;"
              v-on:click="removeProp(prop)"
            >
              <i class="delete icon"></i>
              {{ prop.name }}
            </button>
          </div>
        </div>

        <h2>Talent</h2>

        <div class="ui right labeled left icon input">
          <i class="users icon"></i>
          <input
            type="text"
            placeholder="Enter Talent"
            id="ActorTags"
            v-model="talentInput"
            v-on:keyup.enter="addTalent(talentInput)"
          >
          <a class="ui tag label" v-on:click="addTalent(talentInput)">Add Actor/Actress</a>
        </div>

        <div class="ui grid n-padding">
          <div v-for="actor in talent">
            <button
              class="ui labeled icon button mini"
              style="margin-top: 12px;"
              v-on:click="removeTalent(actor)"
            >
              <i class="delete icon"></i>
              {{ actor.name }}
            </button>
          </div>
        </div>

        <h2>Locations</h2>

        <div class="ui right labeled left icon input">
          <i class="map marker alternate icon"></i>
          <input
            type="text"
            placeholder="Enter Locations"
            id="LocationTags"
            v-model="locationInput"
            v-on:keyup.enter="addLocation(locationInput)"
          >
          <a class="ui tag label" v-on:click="addLocation(locationInput)">Add Location</a>
        </div>

        <div class="ui grid n-padding">
          <div v-for="place in location">
            <button
              class="ui labeled icon button mini"
              style="margin-top: 12px;"
              v-on:click="removeLocation(place)"
            >
              <i class="delete icon"></i>
              {{ place.name }}
            </button>
          </div>
        </div>
        <br>
        <br>
        <button class="ui button primary" v-on:click="generateProd">Generate</button>
      </div>
    </div>
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

$(window).scroll(function() {
  $(".header").css("opacity", 1 - $(window).scrollTop() / 500);
});

export default {
  name: "generate",
  components: {},
  data() {
    return {
      totalShots: 1,
      propInput: "",
      props: [],
      talentInput: "",
      talent: [],
      locationInput: "",
      location: []
    };
  },
  methods: {
    // Generate Production Schedule
    generateProd: function(e) {
      const doc = new Document();
      var totalShotsFromUI = parseInt(this.totalShots);
      totalShotsFromUI += 1;
      const text = new TextRun("Production Schedule").font("Arial");
      const paragraph = new Paragraph()
        .heading1()
        .center()
        .spacing({ after: 120 });
      paragraph.addRun(text);
      doc.addParagraph(paragraph);

      const table = doc.createTable(totalShotsFromUI, 5);
      table.getCell(0, 0).addContent(new Paragraph("Shot Number"));
      table.getCell(0, 1).addContent(new Paragraph("Shot Time"));
      table.getCell(0, 2).addContent(new Paragraph("Props"));
      table.getCell(0, 3).addContent(new Paragraph("Location"));
      table.getCell(0, 4).addContent(new Paragraph("Talent"));

      var shotcount = 1;
      for (shotcount; shotcount < totalShotsFromUI; shotcount++) {
        table
          .getCell(shotcount, 0)
          .addContent(new Paragraph(shotcount.toString()));
      }
      const packer = new Packer();

      packer.toBlob(doc).then(blob => {
        console.log(blob);
        saveAs(blob, "ProductionSchedule.docx");
        console.log("Document created successfully");
      });
    },

    // Prop List
    addProp: function(e) {
      if (e == "") return;
      this.props.push({ name: e });
      this.propInput = "";
    },
    removeProp: function(e) {
      this.props.splice(this.props.indexOf(e), 1);
    },

    // Talent List
    addTalent: function(e) {
      if (e == "") return;
      this.talent.push({ name: e });
      this.talentInput = "";
    },
    removeTalent: function(e) {
      this.talent.splice(this.talent.indexOf(e), 1);
    },

    // Location List
    addLocation: function(e) {
      if (e == "") return;
      this.location.push({ name: e, shots: [] });
      this.locationInput = "";
    },
    removeLocation: function(e) {
      this.location.splice(this.location.indexOf(e), 1);
    }
  }
};
</script>

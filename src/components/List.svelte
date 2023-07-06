<script>
    let items = [
      {
        title: 'Learn how to Eco-Drive',
        details: [
          'Approach intersections at a slower speed! This reduces the need to stop at or accelerate after the light.'
        ]
      },
      {
        title: 'Spread the Word',
        details: [
          'Eco-driving works best when more people are participating, so tell your friends about eco-driving!',
          'Share this tool so they can see eco-driving’s potential!'
        ]
      },
      {
        title: 'Reach out to Your Local Transportation Officials',
        details: [
            "Let your local department of transportation know that you are interested in eco-driving so that they can prioritize its implementation",
            "Encourage your local officials to take advantage of grants for reducing emissions in the Inflation Reduction act like the Carbon Reduction Program.",
            "Contact information for the Department of Transportation for each city and sample email templates are available here."
        ]
      },
      {
        title: 'Contact your Representatives',
        details: [
            "Eco-driving requires public investment to make traffic signal timing available to you and your vehicle. Tell your local and national representatives that you want to prioritize this public investment.",
            "Encourage your representatives to tackle climate change and invest in solutions like eco-driving.",
            "Contact information for the representatives for each city and sample email templates are available here."
        ]
      }
    ];
  </script>
  
  <style>
    .item {
      margin-bottom: 1rem;
      text-align: left;
      margin-left: 1rem;
    }
  
    .details {
      margin-top: 0.5rem;
      margin-left: 2rem;
      color: gray;
      text-align: left;
    }
    .header {
    text-align: center;
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }
  </style>
  
  <div>
    <h2 class="header">Tips for eco-driving</h2>
    {#each items as item}
      <div class="item">
        <h3>{item.title}</h3>
        {#each item.details as detail}
          <p class="details">{detail}</p>
        {/each}
      </div>
    {/each}
  </div>
  
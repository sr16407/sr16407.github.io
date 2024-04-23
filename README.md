we must create a new react project:




npx create-react-app my-portfolio

cd my-portfolio




and replace the contents of src/App.js with the provided React code:




import React from 'react';




function App() {

  const smoothScroll = (target, duration) => {

    const targetElement = document.querySelector(target);

    const targetPosition = targetElement.getBoundingClientRect().top;

    const startPosition = window.pageYOffset;

    const distance = targetPosition - startPosition;

    let startTime = null;




    const animation = (currentTime) => {

      if (startTime === null) startTime = currentTime;

      const timeElapsed = currentTime - startTime;

      const run = ease(timeElapsed, startPosition, distance, duration);

      window.scrollTo(0, run);

      if (timeElapsed < duration) requestAnimationFrame(animation);

    };




    const ease = (t, b, c, d) => {

      t /= d / 2;

      if (t < 1) return c / 2 * t * t + b;

      t--;

      return -c / 2 * (t * (t - 2) - 1) + b;

    };




    requestAnimationFrame(animation);

  };




  const handleClick = (e, target) => {

    e.preventDefault();

    smoothScroll(target, 1000);

  };




  return (

    <div>

      <nav>

        <a href="#section1" onClick={(e) => handleClick(e, "#section1")}>Section 1</a>

        <a href="#section2" onClick={(e) => handleClick(e, "#section2")}>Section 2</a>

        <a href="#section3" onClick={(e) => handleClick(e, "#section3")}>Section 3</a>

      </nav>




      <section id="section1" style={{ backgroundColor: 'lightblue' }}>Section 1</section>

      <section id="section2" style={{ backgroundColor: 'lightgreen' }}>Section 2</section>

      <section id="section3" style={{ backgroundColor: 'lightcoral' }}>Section 3</section>

    </div>

  );

}




export default App;




next, i will replace the contents of src/index.js with the provided code:




import React from 'react';

import ReactDOM from 'react-dom';

import App from './App';




ReactDOM.render(

  <React.StrictMode>

    <App />

  </React.StrictMode>,

  document.getElementById('root')

);




now i will remove unnecessary files like src/App.css, src/App.test.js, and src/logo.svg, and run ’npm start’ to start the development server.




Now i will break down the UI  into reusable components. we can identify the distinct parts of the page and create separate components for them:




Navigation Component: This component will represent the navigation bar at the top of the page.

Section Component: This component will represent each section of the page content.

Let's create these components:

Navigation Component (Navigation.js):




import React from 'react';




function Navigation({ handleClick }) {

  return (

    <nav>

      <a href="#section1" onClick={(e) => handleClick(e, "#section1")}>Section 1</a>

      <a href="#section2" onClick={(e) => handleClick(e, "#section2")}>Section 2</a>

      <a href="#section3" onClick={(e) => handleClick(e, "#section3")}>Section 3</a>

    </nav>

  );

}




export default Navigation;




Section Component (Section.js):




import React from 'react';




function Section({ id, backgroundColor, children }) {

  return (

    <section id={id} style={{ backgroundColor }}>

      {children}

    </section>

  );

}




export default Section;




App Component (App.js):




import React from 'react';

import Navigation from './Navigation';

import Section from './Section';




function App() {

  const smoothScroll = (target, duration) => {

    const targetElement = document.querySelector(target);

    const targetPosition = targetElement.getBoundingClientRect().top;

    const startPosition = window.pageYOffset;

    const distance = targetPosition - startPosition;

    let startTime = null;




    const animation = (currentTime) => {

      if (startTime === null) startTime = currentTime;

      const timeElapsed = currentTime - startTime;

      const run = ease(timeElapsed, startPosition, distance, duration);

      window.scrollTo(0, run);

      if (timeElapsed < duration) requestAnimationFrame(animation);

    };




    const ease = (t, b, c, d) => {

      t /= d / 2;

      if (t < 1) return c / 2 * t * t + b;

      t--;

      return -c / 2 * (t * (t - 2) - 1) + b;

    };




    requestAnimationFrame(animation);

  };




  const handleClick = (e, target) => {

    e.preventDefault();

    smoothScroll(target, 1000);

  };




  return (

    <div>

      <Navigation handleClick={handleClick} />

      <Section id="section1" backgroundColor="lightblue">Section 1</Section>

      <Section id="section2" backgroundColor="lightgreen">Section 2</Section>

      <Section id="section3" backgroundColor="lightcoral">Section 3</Section>

    </div>

  );

}




export default App;




Now, each part of the UI is encapsulated within its own component, making it easier to manage and reuse. The Navigation component handles the navigation bar, and the Section component handles the sections of content.




To implement client-side routing in a React application, we can use a routing library like React Router. With React Router, we can define routes for different sections of our single-page application and render the appropriate components based on the current route.




Install React Router:
npm install react-router-dom




Update the App.js file to use React Router:
import React from 'react';

import { BrowserRouter as Router, Route, NavLink } from 'react-router-dom';

import Section from './Section';




function App() {

  const smoothScroll = (target, duration) => {

    const targetElement = document.querySelector(target);

    const targetPosition = targetElement.getBoundingClientRect().top;

    const startPosition = window.pageYOffset;

    const distance = targetPosition - startPosition;

    let startTime = null;




    const animation = (currentTime) => {

      if (startTime === null) startTime = currentTime;

      const timeElapsed = currentTime - startTime;

      const run = ease(timeElapsed, startPosition, distance, duration);

      window.scrollTo(0, run);

      if (timeElapsed < duration) requestAnimationFrame(animation);

    };




    const ease = (t, b, c, d) => {

      t /= d / 2;

      if (t < 1) return c / 2 * t * t + b;

      t--;

      return -c / 2 * (t * (t - 2) - 1) + b;

    };




    requestAnimationFrame(animation);

  };




  const handleClick = (e, target) => {

    e.preventDefault();

    smoothScroll(target, 1000);

  };




  return (

    <Router>

      <div>

        <nav>

          <NavLink to="/section1" onClick={(e) => handleClick(e, "#section1")}>Section 1</NavLink>

          <NavLink to="/section2" onClick={(e) => handleClick(e, "#section2")}>Section 2</NavLink>

          <NavLink to="/section3" onClick={(e) => handleClick(e, "#section3")}>Section 3</NavLink>

        </nav>




        <Route path="/section1">

          <Section id="section1" backgroundColor="lightblue">Section 1</Section>

        </Route>

        <Route path="/section2">

          <Section id="section2" backgroundColor="lightgreen">Section 2</Section>

        </Route>

        <Route path="/section3">

          <Section id="section3" backgroundColor="lightcoral">Section 3</Section>

        </Route>

      </div>

    </Router>

  );

}




export default App;




In this updated App.js, we're using BrowserRouter as our router, and we define Route components for each section of the page. The NavLink components provide navigation links, and when clicked, they update the URL without causing a full page reload. The Section components are rendered based on the current route.




To fetch project data from a mock API and display it dynamically in our React application, we'll follow these steps:

Create a mock API endpoint or use a mock data service like JSONPlaceholder.
Fetch data from the mock API using fetch or a library like Axios.
Store the fetched data in the React component's state.
Render the fetched data dynamically in the component's JSX.



First I will install Axios:




npm install axios




I will Create a new file named api.js in my src directory to handle API requests:
import axios from 'axios';




const API_URL = 'https://jsonplaceholder.typicode.com';




export const fetchProjects = async () => {

  try {

    const response = await axios.get(`${API_URL}/posts`);

    return response.data;

  } catch (error) {

    console.error('Error fetching projects:', error);

    return [];

  }

};




This file defines a function fetchProjects that fetches project data from a mock API endpoint.

I will Update my App.js file to fetch and display the project data:

import React, { useState, useEffect } from 'react';

import { BrowserRouter as Router, Route, NavLink } from 'react-router-dom';

import Section from './Section';

import { fetchProjects } from './api';




function App() {

  const [projects, setProjects] = useState([]);




  useEffect(() => {

    const fetchProjectsData = async () => {

      const data = await fetchProjects();

      setProjects(data);

    };




    fetchProjectsData();

  }, []);




  return (

    <Router>

      <div>

        <nav>

          <NavLink to="/section1">Section 1</NavLink>

          <NavLink to="/section2">Section 2</NavLink>

          <NavLink to="/section3">Section 3</NavLink>

        </nav>




        <Route path="/section1">

          <Section id="section1" backgroundColor="lightblue">Section 1</Section>

        </Route>

        <Route path="/section2">

          <Section id="section2" backgroundColor="lightgreen">Section 2</Section>

        </Route>

        <Route path="/section3">

          <Section id="section3" backgroundColor="lightcoral">Section 3</Section>

        </Route>




        <div>

          <h2>Projects</h2>

          <ul>

            {projects.map(project => (

              <li key={project.id}>{project.title}</li>

            ))}

          </ul>

        </div>

      </div>

    </Router>

  );

}




export default App;




In this updated App.js, we use the useState and useEffect hooks to fetch the projects data when the component mounts. The fetched data is stored in the projects state variable. We then map over the projects array to dynamically render project titles in a list.




we'll utilize both local state and props. We'll also demonstrate how to update the state and pass data between components using props. Here's how we can achieve this:

Define Stateful Components: We'll define components that hold their own state where necessary.

Pass Data via Props: We'll pass data from parent components to child components using props.

Handle State Updates: We'll handle state updates within components and propagate changes to child components as needed.

Let's update our App.js to demonstrate effective state management:




import React, { useState, useEffect } from 'react';

import { BrowserRouter as Router, Route, NavLink } from 'react-router-dom';

import Section from './Section';

import { fetchProjects } from './api';




function App() {

  const [projects, setProjects] = useState([]);

  const [loading, setLoading] = useState(true); // Track loading state




  useEffect(() => {

    const fetchProjectsData = async () => {

      try {

        const data = await fetchProjects();

        setProjects(data);

        setLoading(false); // Set loading to false after data fetch

      } catch (error) {

        console.error('Error fetching projects:', error);

        setLoading(false); // Set loading to false in case of error

      }

    };




    fetchProjectsData();

  }, []);




  const handleProjectDelete = (id) => {

    // Update the projects state by removing the project with the given id

    setProjects(projects.filter(project => project.id !== id));

  };




  return (

    <Router>

      <div>

        <nav>

          <NavLink to="/section1">Section 1</NavLink>

          <NavLink to="/section2">Section 2</NavLink>

          <NavLink to="/section3">Section 3</NavLink>

        </nav>




        <Route path="/section1">

          <Section id="section1" backgroundColor="lightblue">Section 1</Section>

        </Route>

        <Route path="/section2">

          <Section id="section2" backgroundColor="lightgreen">Section 2</Section>

        </Route>

        <Route path="/section3">

          <Section id="section3" backgroundColor="lightcoral">Section 3</Section>

        </Route>




        {loading ? (

          <div>Loading...</div>

        ) : (

          <div>

            <h2>Projects</h2>

            <ul>

              {projects.map(project => (

                <li key={project.id}>

                  {project.title}

                  <button onClick={() => handleProjectDelete(project.id)}>Delete</button>

                </li>

              ))}

            </ul>

          </div>

        )}

      </div>

    </Router>

  );

}




export default App;




In this updated App.js:

We use the useState hook to manage the state of projects and loading.
We fetch projects data asynchronously and update the state accordingly.
We conditionally render either a loading message or the list of projects based on the loading state.
We pass the handleProjectDelete function as a prop to the Section component, which allows deleting projects.





   

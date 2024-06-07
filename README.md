import React, { useState } from 'react';
import { BrowserRouter as Router, Route, Switch, Link, Redirect } from 'react-router-dom';

function App() {
  return (
    <Router>
      <Switch>
        <Route exact path="/" component={RegistrationForm} />
        <Route exact path="/success" component={SuccessPage} />
        <Redirect to="/" />
      </Switch>
    </Router>
  );
}

function RegistrationForm() {
  const [formData, setFormData] = useState({
    firstName: '',
    lastName: '',
    username: '',
    email: '',
    password: '',
    phone: '',
    country: '',
    city: '',
    panNo: '',
    aadharNo: '',
  });

  const [errors, setErrors] = useState({});
  const [submitted, setSubmitted] = useState(false);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData({ ...formData, [name]: value });
    setErrors({ ...errors, [name]: '' }); // Clear the error when user starts typing
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const newErrors = validateForm(formData);
    setErrors(newErrors);
    if (Object.keys(newErrors).length === 0) {
      setSubmitted(true);
    }
  };

  const validateForm = (data) => {
    const errors = {};
    if (!data.firstName) errors.firstName = 'First Name is required';
    if (!data.lastName) errors.lastName = 'Last Name is required';
    if (!data.username) errors.username = 'Username is required';
    if (!data.email) errors.email = 'Email is required';
    if (!data.password) errors.password = 'Password is required';
    if (!data.phone) errors.phone = 'Phone number is required';
    if (!data.country) errors.country = 'Country is required';
    if (!data.city) errors.city = 'City is required';
    if (!data.panNo) errors.panNo = 'Pan No. is required';
    if (!data.aadharNo) errors.aadharNo = 'Aadhar No. is required';
    return errors;
  };

  if (submitted) {
    return <Redirect to="/success" />;
  }

  return (
    <div>
      <h2>Registration Form</h2>
      <form onSubmit={handleSubmit}>
        <div>
          <label>First Name:</label>
          <input type="text" name="firstName" value={formData.firstName} onChange={handleChange} />
          {errors.firstName && <span>{errors.firstName}</span>}
        </div>
        {/* Other input fields */}
        <button type="submit" disabled={Object.keys(errors).length > 0}>Submit</button>
      </form>
    </div>
  );
}

function SuccessPage({ location }) {
  return (
    <div>
      <h2>Registration Successful</h2>
      <p>Details submitted:</p>
      <pre>{JSON.stringify(location.state.formData, null, 2)}</pre>
      <Link to="/">Go Back</Link>
    </div>
  );
}

export default App;
- 👋 Hi, I’m @RichaChakra
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
RichaChakra/RichaChakra is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

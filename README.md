# faker-pk
![PyPI Version](https://img.shields.io/pypi/v/faker-pk)
![PyPI downloads](https://img.shields.io/pypi/dm/faker-pk)
![Python Version](https://img.shields.io/pypi/pyversions/faker-pk)


`faker-pk` is a Python package that generates realistic Pakistani data for testing, software demos, synthetic datasets, and application development.  

It supports generating localized Pakistani names, CNICs, mobile numbers, network providers, complete addresses, bank info, IBANs, company details, industry-aware job titles, clean salary figures, and educational institutions with student profiles.

It also fully integrates as a **Faker Provider** so you can seamlessly use it inside the standard `faker` library ecosystem.

---

## Authors

- **Muhammad Khubaib Ahmad** (`khubaib.ahmad@inference-lab.org`) - Original creator of `faker-pk`
- **INFERENCE Lab** (`contact@inference-lab.org`) - Organization

## Maintainers
- **Ayesha Anwar** (`hayesha1744@gmail.com`) - Lead developer of `faker-pk` v2.0
- **INFERENCE Lab** (`contact@inference-lab.org`) - Project organization

---

## Why Use `faker-pk`?

Developers building Pakistani software applications often encounter issues with:
- Generating realistic, localized user profiles (CNIC, phone numbers, addresses)
- Validating Pakistani identity formats (CNIC last-digit gender checks)
- Populating development databases with real-world company, industry, and banking data
- Simulating student datasets filtered by city, province, or institution level
- Running software demonstrations safely without exposing real personal data

`faker-pk` resolves this by utilizing an optimized, local SQLite database backend for reliable and realistic Pakistani data generation.

---

## Installation

```bash
pip install faker-pk
```

To upgrade to the latest version:

```bash
pip install --upgrade faker-pk
```

---

## Quick Start (Standalone `FakerPK` Class)

```python
from faker_pk import FakerPK

fake = FakerPK()

print("Male Name:", fake.male_name())
print("CNIC:", fake.cnic(gender="male"))
print("Phone Number:", fake.phone_number(provider="Jazz"))
print("Full Address:", fake.full_address(province="Punjab"))
print("Company:", fake.company_name(industry="IT"))
print("Salary (PKR):", fake.salary(industry="IT"))
print("University:", fake.institution(level="university", city="Lahore"))
```

---

## Complete API Reference

### Personal Information

| Function | Description | Options / Filters | Example Output |
| :--- | :--- | :--- | :--- |
| `male_name(count=1)` | Realistic Pakistani male names | `count` | `"Kamran Qureshi"` |
| `female_name(count=1)` | Realistic Pakistani female names | `count` | `"Laraib Javed"` |
| `cnic(count=1, gender=None)` | Valid formatted CNIC `xxxxx-xxxxxxx-x` | `gender='male'/'female'` | `"35201-6543210-7"` |
| `phone_number(count=1, provider=None)` | Pakistani mobile number format | `provider='Jazz'/'Zong'/...` | `"+923001234567"` |
| `sim_provider(count=1)` | Pakistani mobile network operator | `count` | `"Jazz"` |
| `caste(count=1)` | Pakistani castes & surnames | `count` | `"Zehri"` |
| `sect(count=1)` | Religious sects | `count` | `"Sunni"` |
| `dob(count=1)` | Random date of birth | `count` | `"1998-05-14"` |

---

### Address Information

| Function | Description | Options / Filters | Example Output |
| :--- | :--- | :--- | :--- |
| `city(count=1, province=None)` | Pakistani cities | `province='Punjab'/...` | `"Lahore"` |
| `province(count=1, city=None)` | Pakistani provinces | `city='Karachi'/...` | `"Sindh"` |
| `full_address(count=1, city=None, province=None)` | Complete street address with postal code | `city`, `province` | `"House No. 454, Street No. 11, Lahore, Punjab, 54000"` |

---

### Company & Financial Information

| Function | Description | Options / Filters | Example Output |
| :--- | :--- | :--- | :--- |
| `company_name(count=1, industry=None)` | Registered Pakistani business names | `industry='IT'/...` | `"Lucky Cement Limited"` |
| `industry_name(count=1)` | Industry sector names | `count` | `"Information Technology"` |
| `bank_name(count=1)` | Registered commercial banks in Pakistan | `count` | `"Meezan Bank"` |
| `iban(count=1, bank=None)` | Valid Pakistani IBAN format | `bank='HBL'/...` | `"PK27UNIL8060952103358359"` |
| `salary(count=1, industry=None)` | Realistic salary in PKR| `industry='IT'/...` | `115500` |

#### Supported Industry Codes & Names:
When filtering `company_name()`, `job_title()`, or `salary()`, you can pass any of the following codes or full names:

- `IT` (Information Technology)
- `Finance` (Finance & Banking)
- `Healthcare` (Healthcare & Pharmaceuticals)
- `Education` (Education & Academics)
- `Marketing` (Marketing & Media)
- `Government` (Government & Public Sector)
- `Engineering` (Engineering & Manufacturing)
- `Retail` (Hospitality & Retail)
- `Entrepreneur` (Entrepreneur & Startups)
- `Consulting` (Legal & Consulting)
- `Art` (Art & Entertainment)
- `Politics` (Politics & Public Policy)
- `Agriculture` (Agriculture & Farming)
- `Services` (Domestic & Personal Services)
- `Defense` (Defense & Public Safety)

---

### Job Information

| Function | Description | Options / Filters | Example Output |
| :--- | :--- | :--- | :--- |
| `job_title(count=1, industry=None)` | Industry-specific job titles | `industry='IT'/...` | `"Software Engineer"` |
| `job_title_with_industry(count=1)` | Combined job title and industry code | `count` | `"Data Scientist - IT"` |

---

### Education & Student Profiles

| Function | Description | Options / Filters | Example Output |
| :--- | :--- | :--- | :--- |
| `institution(count=1, level=None, city=None, province=None)` | Pakistani school, college, or university | `level='school'/'college'/'university'`, `city`, `province` | `"LUMS"` |
| `student_dob(count=1, level='university')` | Age-appropriate student DOB | `level='school'/'college'/'university'` | `2002-05-24` |
| `student_profile(count=1, level=None, province=None)` | Complete, coherent student dict profile | `level`, `province` | `{'name': 'Shahzaib Mirwani', 'gender': 'male', 'cnic': '36836-2572000-5', 'institution': 'University of Karachi', 'level': 'university', 'city': 'Karachi', 'province': 'Sindh', 'dob': 2002-05-24}` |

---

## Generating Multiple Records

Passing `count > 1` returns a list of items:

```python
from faker_pk import FakerPK

fake = FakerPK()

# Generate 3 cities in Sindh
print(fake.city(count=3, province="Sindh"))
# Output: ['Karachi', 'Hyderabad', 'Sukkur']

# Generate 5 realistic student profiles
profiles = fake.student_profile(count=5, level="university")
```

---

## Standard `faker` Integration (`FakerPKProvider`)

You can register `FakerPKProvider` with Python's standard `faker` library. All methods are available prefixed with `pk_` (or as alias methods):

```python
from faker import Faker
from faker_pk import FakerPKProvider

fake = Faker()
fake.add_provider(FakerPKProvider)

print(fake.pk_male_name())
print(fake.pk_cnic(gender="male"))
print(fake.pk_full_address(province="Punjab"))
print(fake.pk_institution(level="university"))
print(fake.pk_student_profile())
```

---

## Local Development & Testing

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Inference-LAB/faker-pk.git
   cd faker-pk
   ```

2. **Install in editable mode**:
   ```bash
   pip install -e .
   ```

3. **Run the test suite**:
   ```bash
   pytest
   ```

---

## Contributing

We welcome contributions from the community! Whether you are expanding datasets, adding validation rules, or improving performance, here is how you can help:

#### How to Contribute:
1. **Fork & Clone**: Fork `Inference-LAB/faker-pk` on GitHub and clone your fork locally.
2. **Feature Branches**: Create a dedicated feature branch for your changes (`git checkout -b feat/add-new-dataset`).
3. **Database Updates**: If adding new dataset records, update `faker_pk/initialize_db.py` so the SQLite database re-seeds cleanly.
4. **Write Unit Tests**: Add tests under `tests/` for any new functions or parameters. Ensure `pytest` passes with 100% success.
5. **Submit a Pull Request**: Push your branch and open a PR against `main` with a clear summary of your changes.

---

## Authors & Contact Info

### **Muhammad Khubaib Ahmad**
- **Email**: [khubaib.ahmad@inference-lab.org](mailto:khubaib.ahmad@inference-lab.org)
- **GitHub**: [Khubaib8281](https://github.com/Khubaib8281)
- **PyPI**: [Khubaib_01](https://pypi.org/project/faker-pk)
- **LinkedIn**: [Muhammad Khubaib Ahmad](https://www.linkedin.com/in/muhammad-khubaib-ahmad-/)

### **Ayesha Anwar**
- **Email**: [hayesha1744@gmail.com](mailto:hayesha1744@gmail.com)
- **GitHub**: [Ayesha-Anwar607](https://github.com/Ayesha-Anwar607)
- **LinkedIn**: [Ayesha Anwar](https://www.linkedin.com/in/ayesha-anwar-3b73b8349/)

---

## License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

## Support

If `faker-pk` was helpful for your project or application, please consider giving the repository a star on GitHub!  
 [https://github.com/Inference-LAB/faker-pk](https://github.com/Inference-LAB/faker-pk)


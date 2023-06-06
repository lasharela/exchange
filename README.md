# exchange
# exchange
export const withoutDecimalRegex = (value: string) => {
  return value
    .toString()
    .replace(/[^0-9]/g, "")
    .replace(/\B(?=(\d{3})+(?!\d))/g, ",");
};

==
export const replaceInvalidMonthOfYearChars = (value: string) => value.replaceAll(/([ |M|Y])/g, ""); // dry ui value has extra space MM / YYYY

Remove duplicates in this character class.
==

export const postalCodeRegex = (value: string): string => {
  let PostalCodeRegexArr = value.replace(/[^A-Za-z0-9]/g, "").match(/(.{0,14})/);
  return PostalCodeRegexArr[1];
};

export const cityProvinceRegex = (value: string): string => {
  let cityProvinceRegexArr = value.replace(/^[-'\s]|[^A-Za-z0-9 ',]/g, "").match(/(.{0,24})/);
  return cityProvinceRegexArr[1];
};

export const zipCodeRegex = (value: string): string => {
  let zipCodeRegexArr = value.replace(/\D/g, "").match(/(\d{0,5})/);
  return zipCodeRegexArr[1];
};

export const containsPOBox = (value: string): boolean => {
  let addressValue = value ? value.replace(/[^a-z0-9\s]/gi, "").replace(/[_\s]/g, "") : "";
  addressValue = addressValue.toLowerCase();

  if (addressValue.indexOf("pobox") >= 0 || addressValue.indexOf("postofficebox") >= 0) {
    return true;
  } else {
    return false;
  }
};

export const isZipValid = (value: string): boolean => {
  return !/^0*$/.test(value);
};
==

export const emailMask = {
  mask: /^(?!.*\.\.|\.|\s)[a-zA-Z0-9.!$%#&'^*+/=?_{|}~\s-]+@?(?!\.|-)[a-zA-Z0-9.-]*(?:\.?[a-zA-Z0-9]*)*$/
};

export const emailMask = {
  mask: /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(\.[a-zA-Z0-9-]+)*$/
};

Make sure the regex used here, which is vulnerable to super-linear runtime due to backtracking, cannot lead to denial of service.
Comment

export const withoutDecimalRegex = (value: string) => {
  return value
    .toString()
    .replace(/[^0-9]/g, "")
    .replace(/\B(?=(\d{3})+(?!\d))/g, ",");
};

Make sure the regex used here, which is vulnerable to super-linear runtime due to backtracking, cannot lead to denial of service.
Comment

===
const { mask } = require('./path-to-emailMask-file');

describe('Email Validation', () => {

  // Test valid emails
  it('should validate valid email addresses', () => {
    const validEmails = [
      'email@example.com',
      'firstname.lastname@example.com',
      'email@subdomain.example.com',
      'firstname+lastname@example.com',
      'email@123.123.123.123',
      '1234567890@example.com',
      'email@example-one.com',
      '_______@example.com',
      'email@example.name',
      'email@example.museum',
      'email@example.co.jp',
      'firstname-lastname@example.com'
    ];

    validEmails.forEach(email => {
      expect(mask.test(email)).toBeTruthy();
    });
  });

  // Test invalid emails
  it('should not validate invalid email addresses', () => {
    const invalidEmails = [
      'plainaddress',
      '@no-local-part.com',
      'Outlook Contact <outlook-contact@outlook.com>',
      'no-at-sign.net',
      'no-tld@test',
      'double..dot@test.com',
      'double.@test.com',
      '.leading-dot@test.com',
      'spaces in local@test.com',
      'spaces in domain@test .com',
      'spaces in both@test . com'
    ];

    invalidEmails.forEach(email => {
      expect(mask.test(email)).toBeFalsy();
    });
  });

});

export const emailMask = {
    mask: /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(\.[a-zA-Z0-9-]+)+$/

};

    ✕ should not validate invalid email addresses: double..dot@test.com (2 ms)
    ✕ should not validate invalid email addresses: double.@test.com (1 ms)
    ✕ should not validate invalid email addresses: .leading-dot@test.com (1 ms)
    
    
    export const emailMask = {
  mask: /^(?!.*\.\.)[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$/
};



AC2: E-mail Address field should be a required text box field with maximum of 255 characters, which follows these validation rules:

o    Support: Alphanumeric (a-z, A-Z, 0-9) 
 o    Special characters allowed prior to @ sign (userID):   | ! ~ / # $ % & ' * + = ? ^ _ { } - .
 o    Special characters allowed after @ sign (domain):   - . (not first or last character)
            If user types - or . after @ sign with no character following it, error should be displayed "Please enter a valid email address following the format name@example.com"
 o    Special characters NOT allowed:  ` \ ( ) < > "  [ ]
 o    Cannot start with a period
 o    Allowable character, letter or number must follow a period
 o    Cannot have 2 consecutive periods
 o    Cannot start or end with a space
 o    Space is allowed in body prior to @ sign
 o    Maximum 255 characters
 o    Require at least one @ symbol and one period
 o    Required format: userID@domain.com 
 NOTE: Special characters which are NOT allowed should not be allowed to be typed into the field
 
 
 
 describe("Email Validation", () => {
  // Test valid emails

  test.each([
    ["email@example.com", true],
    ["firstname.lastname@example.com", true],
    ["email@subdomain.example.com", true],
    ["firstname+lastname@example.com", true],
    ["1234567890@example.com", true],
    ["email@example-one.com", true],
    ["_______@example.com", true],
    ["email@example.museum", true],
    ["firstname-lastname@example.com", true]
  ])("should be correct email: %s", (email, expected) => expect(emailMask.mask.test(email)).toBe(expected));

  test.each([
    ["plainaddress", false],
    ["@no-local-part.com", false],
    ["Outlook Contact <outlook-contact@outlook.com>", false],
    ["no-at-sign.net", false],
    ["double..dot@test.com", false],
    ["double.@test.com", false],
    [".leading-dot@test.com", false],
    ["spaces in local@test.com", false],
    ["spaces in domain@test .com", false],
    ["spaces in both@test . com", false]
  ])("should not validate invalid email addresses: %s", (email, expected) =>
    expect(emailMask.mask.test(email)).toBe(expected)
  );
});

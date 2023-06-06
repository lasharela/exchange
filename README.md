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

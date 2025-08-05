class Solution {
public:
    int numUniqueEmails(vector<string>& emails) {
        unordered_set<string> uniqueEmails;

        for (string email : emails) {
            string local;
            string domain;
            bool plusFound = false;
            bool atFound = false;

            for (char c : email) {
                if (c == '@') {
                    atFound = true;
                }
                if (atFound) {
                    domain += c; // keep domain part unchanged
                } else {
                    if (c == '+') {
                        plusFound = true; // ignore characters after '+'
                    } else if (!plusFound && c != '.') {
                        local += c; // keep character if not '.' and before '+'
                    }
                }
            }
            uniqueEmails.insert(local + domain);
        }
        return uniqueEmails.size();
    }
};
